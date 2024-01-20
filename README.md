local hub = Instance.new("Frame")

hub.Size = UDim2.new(0.2, 0, 0.2, 0)
hub.Position = UDim2.new(0.8, 0, 0.8, 0)
hub.Parent = workspace

local button = Instance.new("Open")

button.Size = UDim2.new(0.2, 0, 0.1, 0)
button.Position = UDim2.new(0.8, 0, 0.7, 0)
button.Text = "Abrir Hub"

button.Parent = hub

button.Activated:Connect(function()
  -- Abre o hub.
end)

local button2 = Instance.new("Close")

button2.Size = UDim2.new(0.2, 0, 0.1, 0)
button2.Position = UDim2.new(0.8, 0, 0.6, 0)
button2.Text = "Pegar Sucata"

button2.Parent = hub

button2.Activated:Connect(function()
  -- Obtém a posição do jogador.
  local playerPosition = player.Character.HumanoidRootPart.Position

  -- Percorre todas as sucatas.
  for _, scrap in pairs(workspace:GetChildren()) do
    if scrap.Name == "UnderwaterScrap" then
      -- Verifica se a sucata está próxima do jogador.
      local distance = (scrap.Position - playerPosition).Magnitude

      if distance <= 5 then
        -- Pega os itens da sucata.
        pickUpScrap(scrap)

        -- Se o inventário estiver cheio, para de pegar itens.
        if player.Backpack:FindFirstChild("Item") then
          break
        end
      end
    end
  end
end)

local button3 = Instance.new("Idk")

button3.Size = UDim2.new(0.2, 0, 0.1, 0)
button3.Position = UDim2.new(0.8, 0, 0.5, 0)
button3.Text = "Ir pra Nave"

button3.Parent = hub

button3.Activated:Connect(function()
  -- Teleporta o jogador para a nave.
  teleportToShip()
end)

function pickUpScrap(scrap)
  -- Verifica se a sucata tem um botão.
  if scrap:FindFirstChild("Button") then
    -- Clica no botão.
    scrap.Button.Activated:Fire()
  end
end

function teleportToShip()
  -- Teleporta o jogador para a nave.
  player.Character:Teleport(game.Workspace.Ships["Minha Nave"].Position)
end
