````markdown
# Guia de API do Roblox para Iniciantes

Este documento resume os conceitos e referências mais importantes da API do Roblox Studio, em formato Markdown para facilitar seu aprendizado no GitHub.

---

## Índice

1. [Introdução ao Roblox e Lua](#introdu%C3%A7%C3%A3o-ao-roblox-e-lua)
2. [Configuração Inicial](#configura%C3%A7%C3%A3o-inicial)
3. [Conceitos Fundamentais](#conceitos-fundamentais)
   - Instâncias
   - Propriedades
   - Métodos
   - Eventos
4. [Serviços Importantes](#servi%C3%A7os-importantes)
5. [Classes Comuns](#classes-comuns)
6. [Sintaxe e Palavras-chave Lua](#sintaxe-e-palavras-chave-lua)
7. [Manipulação de Eventos](#manipula%C3%A7%C3%A3o-de-eventos)
8. [UI e GuiObjects](#ui-e-guiobjects)
9. [CFrame, Vector3 e Posicionamento](#cframe-vector3-e-posicionamento)
10. [DataStore e Salvamento](#datastore-e-salvamento)
11. [Boas Práticas e Dicas](#boas-pr%C3%A1ticas-e-dicas)

---

## Introdução ao Roblox e Lua

- **Roblox Studio**: ambiente de desenvolvimento para criar jogos e experiências no Roblox.
- **Lua**: linguagem de script leve usada no Roblox. Variante customizada chamada **Luau**.

---

## Configuração Inicial

1. Abra o Roblox Studio.
2. Crie um novo projeto (Baseplate ou outro template).
3. No Explorer, adicione um **Script** dentro de `ServerScriptService` para scripts do servidor ou em `StarterPlayerScripts` para scripts do cliente.
4. Abra o script e comece a digitar em Lua.

```lua
print("Olá, mundo!")
````

---

## Conceitos Fundamentais

### Instâncias

* Tudo no Roblox é uma `Instance`.
* Criar uma instância:

  ```lua
  local part = Instance.new("Part")
  part.Parent = workspace
  ```

### Propriedades

* Cada instância tem propriedades (ex.: `Position`, `Size`, `Name`).
* Alterar propriedade:

  ```lua
  part.Name = "MeuBloco"
  part.Size = Vector3.new(4, 1, 2)
  ```

### Métodos

* Funções próprias de cada classe (ex.: `:Destroy()`, `:Clone()`).

  ```lua
  local copia = part:Clone()
  copia.Parent = workspace
  ```

### Eventos

* Conectam ações a funções (ex.: `Touched`, `Changed`).

  ```lua
  part.Touched:Connect(function(hit)
      print("Colidiu com", hit.Name)
  end)
  ```

---

## Serviços Importantes

| Serviço                        | Descrição                                         |
| ------------------------------ | ------------------------------------------------- |
| `game:GetService("Workspace")` | Mundo 3D onde ficam `Parts` e modelos.            |
| `Players`                      | Jogadores conectados.                             |
| `ReplicatedStorage`            | Armazena objetos compartilhados cliente/servidor. |
| `ServerScriptService`          | Scripts do lado do servidor.                      |
| `StarterGui`                   | GuiObjects que herdam para cada jogador.          |
| `DataStoreService`             | Salvar dados persistentes.                        |
| `TweenService`                 | Animações suaves de propriedades.                 |
| `GuiService`                   | Controle de interfaces de usuário.                |

---

## Classes Comuns

* **Part**: bloco básico.
* **Model**: grupo de instâncias.
* **Humanoid**: controla personagens.
* **CFrame**: orientação/posição 3D.
* **Vector3**: coordenadas XYZ.
* **UDim2**: tamanhos e posições de GUI.
* **ScreenGui**, **Frame**, **TextLabel**, **TextButton**: elementos de interface.

---

## Sintaxe e Palavras-chave Lua

* **Variáveis**: `local x = 10`
* **Funções**:

  ```lua
  local function saudacao(nome)
      print("Olá, "..nome)
  end
  saudacao("Jogador")
  ```
* **Laços**:

  ```lua
  for i = 1, 5 do
      print(i)
  end

  while task.wait(1) do
      print("A cada segundo")
  end
  ```
* **Controle de fluxo**: `if`, `elseif`, `else`, `break`, `return`

---

## Manipulação de Eventos

* Conectar evento:

  ```lua
  game.Players.PlayerAdded:Connect(function(player)
      print(player.Name, "entrou no jogo")
  end)
  ```
* Alguns eventos úteis:

  * `PlayerRemoving`
  * `CharacterAdded`
  * `DescendantAdded` / `DescendantRemoving`

---

## UI e GuiObjects

1. Adicione um `ScreenGui` em `StarterGui`.
2. Dentro dele, crie `Frame`, `TextLabel`, `TextButton`, etc.
3. Propriedades principais: `Position`, `Size`, `BackgroundColor3`, `Text`.

```lua
local screenGui = Instance.new("ScreenGui", game.Players.LocalPlayer:WaitForChild("PlayerGui"))
local button = Instance.new("TextButton")
button.Parent = screenGui
button.Size = UDim2.new(0, 200, 0, 50)
button.Position = UDim2.new(0.5, -100, 0.5, -25)
button.Text = "Clique"
button.MouseButton1Click:Connect(function()
    print("Botão clicado")
end)
```

---

## CFrame, Vector3 e Posicionamento

* **Vector3.new(x, y, z)**: posição ou tamanho.
* **CFrame.new(x, y, z)**: posição + orientação.
* Combinações:

  ```lua
  part.CFrame = CFrame.new(0, 5, 0) * CFrame.Angles(0, math.rad(45), 0)
  ```

---

## DataStore e Salvamento

```lua
local DataStoreService = game:GetService("DataStoreService")
local ds = DataStoreService:GetDataStore("MeuDataStore")

-- Salvar
ds:SetAsync(player.UserId.."_moedas", 100)

-- Ler
local sucesso, valor = pcall(function()
    return ds:GetAsync(player.UserId.."_moedas")
end)
if sucesso then
    print("Moedas lidas:", valor)
end
```

---

## Boas Práticas e Dicas

* Sempre use `local` para variáveis e funções.
* Prefira `task.wait()` a `wait()`.
* Gerencie erros com `pcall`.
* Separe scripts do cliente/servidor corretamente.
* Documente seu código com comentários.

---

*Este guia oferece um panorama inicial. Para referência completa, visite a [API Reference oficial do Roblox](https://create.roblox.com/docs/reference).*

```
```
