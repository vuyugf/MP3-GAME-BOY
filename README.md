-- Services
local SoundService = game:GetService("SoundService")
local HttpService = game:GetService("HttpService")
local CoreGui = game:GetService("CoreGui")

-- Destruir GUI anterior se existir
if CoreGui:FindFirstChild("GameBoyXMP3Gui") then
    CoreGui.GameBoyXMP3Gui:Destroy()
end

-- ScreenGui Principal
local ScreenGui = Instance.new("ScreenGui")
ScreenGui.Name = "GameBoyXMP3Gui"
ScreenGui.ResetOnSpawn = false

if syn and syn.protect_gui then
    syn.protect_gui(ScreenGui)
    ScreenGui.Parent = CoreGui
elseif gethui then
    ScreenGui.Parent = gethui()
else
    ScreenGui.Parent = CoreGui
end

----------------------------------------------------
-- GERENCIADOR DE ÁUDIO
----------------------------------------------------
local currentSound = Instance.new("Sound")
currentSound.Name = "GameBoyX_MP3Player"
currentSound.Parent = SoundService

----------------------------------------------------
-- BOTÃO FLUTUANTE (BOLINHA COM LOGO MP3)
----------------------------------------------------
local ToggleButton = Instance.new("TextButton")
local UICornerBtn = Instance.new("UICorner")
local UIStrokeBtn = Instance.new("UIStroke")

ToggleButton.Name = "ToggleButton"
ToggleButton.Size = UDim2.new(0, 60, 0, 60)
ToggleButton.Position = UDim2.new(0.05, 0, 0.4, 0)
ToggleButton.BackgroundColor3 = Color3.fromRGB(15, 15, 15)
ToggleButton.Active = true
ToggleButton.Draggable = true
ToggleButton.Text = "MP3"
ToggleButton.TextColor3 = Color3.fromRGB(85, 255, 0)
ToggleButton.Font = Enum.Font.SourceSansBold
ToggleButton.TextSize = 20
ToggleButton.Parent = ScreenGui

UICornerBtn.CornerRadius = UDim.new(1, 0)
UICornerBtn.Parent = ToggleButton

UIStrokeBtn.Color = Color3.fromRGB(85, 255, 0)
UIStrokeBtn.Thickness = 2
UIStrokeBtn.Parent = ToggleButton

----------------------------------------------------
-- PAINEL PRINCIPAL (GAMEBOYX MP3)
----------------------------------------------------
local MainFrame = Instance.new("Frame")
local UICornerMain = Instance.new("UICorner")
local Title = Instance.new("TextLabel")
local CloseButton = Instance.new("TextButton")

MainFrame.Name = "MainFrame"
MainFrame.Size = UDim2.new(0, 370, 0, 350)
MainFrame.Position = UDim2.new(0.5, -185, 0.5, -175)
MainFrame.BackgroundColor3 = Color3.fromRGB(20, 20, 20)
MainFrame.Visible = true
MainFrame.Active = true
MainFrame.Draggable = true
MainFrame.Parent = ScreenGui

UICornerMain.CornerRadius = UDim.new(0, 10)
UICornerMain.Parent = MainFrame

-- Título Principal "GameBoyX MP3"
Title.Name = "Title"
Title.Size = UDim2.new(1, -50, 0, 45)
Title.Position = UDim2.new(0, 15, 0, 0)
Title.BackgroundTransparency = 1
Title.Text = "GameBoy<font color=\"rgb(85,255,0)\">X MP3</font>"
Title.RichText = true
Title.TextColor3 = Color3.fromRGB(255, 255, 255)
Title.TextSize = 22
Title.Font = Enum.Font.SourceSansBold
Title.TextXAlignment = Enum.TextXAlignment.Left
Title.Parent = MainFrame

-- Botão Fechar
CloseButton.Name = "CloseButton"
CloseButton.Size = UDim2.new(0, 30, 0, 30)
CloseButton.Position = UDim2.new(1, -35, 0, 8)
CloseButton.BackgroundTransparency = 1
CloseButton.Text = "X"
CloseButton.TextColor3 = Color3.fromRGB(255, 85, 85)
CloseButton.TextSize = 18
CloseButton.Font = Enum.Font.SourceSansBold
CloseButton.Parent = MainFrame

----------------------------------------------------
-- ÁREA MP3
----------------------------------------------------
local MP3Frame = Instance.new("Frame")
local UICornerMP3 = Instance.new("UICorner")
local IdInput = Instance.new("TextBox")
local NameInput = Instance.new("TextBox")
local AddButton = Instance.new("TextButton")
local SaveButton = Instance.new("TextButton")
local ScrollList = Instance.new("ScrollingFrame")
local UIListLayout = Instance.new("UIListLayout")

MP3Frame.Name = "MP3Frame"
MP3Frame.Size = UDim2.new(1, -20, 1, -60)
MP3Frame.Position = UDim2.new(0, 10, 0, 50)
MP3Frame.BackgroundColor3 = Color3.fromRGB(12, 12, 12)
MP3Frame.Parent = MainFrame

UICornerMP3.CornerRadius = UDim.new(0, 8)
UICornerMP3.Parent = MP3Frame

-- Input ID
IdInput.Name = "IdInput"
IdInput.Size = UDim2.new(0, 105, 0, 30)
IdInput.Position = UDim2.new(0, 10, 0, 10)
IdInput.BackgroundColor3 = Color3.fromRGB(28, 28, 28)
IdInput.TextColor3 = Color3.fromRGB(255, 255, 255)
IdInput.PlaceholderText = "ID da Música"
IdInput.PlaceholderColor3 = Color3.fromRGB(140, 140, 140)
IdInput.Font = Enum.Font.SourceSans
IdInput.TextSize = 13
IdInput.Parent = MP3Frame
Instance.new("UICorner", IdInput).CornerRadius = UDim.new(0, 5)

-- Input Nome
NameInput.Name = "NameInput"
NameInput.Size = UDim2.new(0, 115, 0, 30)
NameInput.Position = UDim2.new(0, 120, 0, 10)
NameInput.BackgroundColor3 = Color3.fromRGB(28, 28, 28)
NameInput.TextColor3 = Color3.fromRGB(255, 255, 255)
NameInput.PlaceholderText = "Nome"
NameInput.PlaceholderColor3 = Color3.fromRGB(140, 140, 140)
NameInput.Font = Enum.Font.SourceSans
NameInput.TextSize = 13
NameInput.Parent = MP3Frame
Instance.new("UICorner", NameInput).CornerRadius = UDim.new(0, 5)

-- Botão + (Adicionar)
AddButton.Name = "AddButton"
AddButton.Size = UDim2.new(0, 40, 0, 30)
AddButton.Position = UDim2.new(0, 240, 0, 10)
AddButton.BackgroundColor3 = Color3.fromRGB(85, 255, 0)
AddButton.Text = "+"
AddButton.TextColor3 = Color3.fromRGB(0, 0, 0)
AddButton.Font = Enum.Font.SourceSansBold
AddButton.TextSize = 22
AddButton.Parent = MP3Frame
Instance.new("UICorner", AddButton).CornerRadius = UDim.new(0, 5)

-- Botão Salvar (💾)
SaveButton.Name = "SaveButton"
SaveButton.Size = UDim2.new(0, 45, 0, 30)
SaveButton.Position = UDim2.new(0, 285, 0, 10)
SaveButton.BackgroundColor3 = Color3.fromRGB(35, 120, 255)
SaveButton.Text = "💾"
SaveButton.TextColor3 = Color3.fromRGB(255, 255, 255)
SaveButton.Font = Enum.Font.SourceSansBold
SaveButton.TextSize = 16
SaveButton.Parent = MP3Frame
Instance.new("UICorner", SaveButton).CornerRadius = UDim.new(0, 5)

-- Lista com Scroll (Até 50 Músicas)
ScrollList.Name = "ScrollList"
ScrollList.Size = UDim2.new(1, -20, 1, -55)
ScrollList.Position = UDim2.new(0, 10, 0, 50)
ScrollList.BackgroundTransparency = 1
ScrollList.BorderSizePixel = 0
ScrollList.CanvasSize = UDim2.new(0, 0, 0, 0)
ScrollList.ScrollBarThickness = 4
ScrollList.Parent = MP3Frame

UIListLayout.Parent = ScrollList
UIListLayout.SortOrder = Enum.SortOrder.LayoutOrder
UIListLayout.Padding = UDim.new(0, 6)

----------------------------------------------------
-- LÓGICA DE DADOS E SALVAMENTO
----------------------------------------------------
local savedSongs = {}
local activePlayButton = nil
local playingId = ""
local FILE_PATH = "GameBoyX_MP3_Save.json"

local function createMusicCard(songName, songId, isAutoLoad)
    if #savedSongs >= 50 and not isAutoLoad then
        return
    end

    if not isAutoLoad then
        table.insert(savedSongs, {name = songName, id = songId})
    end

    local ItemRow = Instance.new("Frame")
    ItemRow.Name = "MusicItem"
    ItemRow.Size = UDim2.new(1, -5, 0, 35)
    ItemRow.BackgroundTransparency = 1
    ItemRow.Parent = ScrollList

    -- Quadradinho Nome(id)
    local MusicBox = Instance.new("TextLabel")
    MusicBox.Name = "MusicBox"
    MusicBox.Size = UDim2.new(1, -75, 1, 0)
    MusicBox.Position = UDim2.new(0, 0, 0, 0)
    MusicBox.BackgroundColor3 = Color3.fromRGB(28, 28, 28)
    MusicBox.Text = "  " .. songName .. "(" .. songId .. ")"
    MusicBox.TextColor3 = Color3.fromRGB(255, 255, 255)
    MusicBox.Font = Enum.Font.SourceSans
    MusicBox.TextSize = 14
    MusicBox.TextXAlignment = Enum.TextXAlignment.Left
    MusicBox.TextTruncate = Enum.TextTruncate.AtEnd
    MusicBox.Parent = ItemRow
    Instance.new("UICorner", MusicBox).CornerRadius = UDim.new(0, 6)

    -- Botão Play / Pause (▶ / ⏸)
    local PlayPauseBtn = Instance.new("TextButton")
    PlayPauseBtn.Name = "PlayPauseBtn"
    PlayPauseBtn.Size = UDim2.new(0, 32, 0, 35)
    PlayPauseBtn.Position = UDim2.new(1, -68, 0, 0)
    PlayPauseBtn.BackgroundColor3 = Color3.fromRGB(35, 35, 35)
    PlayPauseBtn.Text = "▶"
    PlayPauseBtn.TextColor3 = Color3.fromRGB(85, 255, 0)
    PlayPauseBtn.Font = Enum.Font.SourceSansBold
    PlayPauseBtn.TextSize = 14
    PlayPauseBtn.Parent = ItemRow
    Instance.new("UICorner", PlayPauseBtn).CornerRadius = UDim.new(0, 6)

    -- Botão Lixeira (🗑️)
    local DeleteBtn = Instance.new("TextButton")
    DeleteBtn.Name = "DeleteBtn"
    DeleteBtn.Size = UDim2.new(0, 32, 0, 35)
    DeleteBtn.Position = UDim2.new(1, -32, 0, 0)
    DeleteBtn.BackgroundColor3 = Color3.fromRGB(40, 20, 20)
    DeleteBtn.Text = "🗑"
    DeleteBtn.TextColor3 = Color3.fromRGB(255, 85, 85)
    DeleteBtn.Font = Enum.Font.SourceSansBold
    DeleteBtn.TextSize = 16
    DeleteBtn.Parent = ItemRow
    Instance.new("UICorner", DeleteBtn).CornerRadius = UDim.new(0, 6)

    -- Evento Play / Pause
    PlayPauseBtn.MouseButton1Click:Connect(function()
        local formattedId = "rbxassetid://" .. songId

        if playingId == formattedId and currentSound.IsPlaying then
            currentSound:Pause()
            PlayPauseBtn.Text = "▶"
            PlayPauseBtn.TextColor3 = Color3.fromRGB(85, 255, 0)
            MusicBox.TextColor3 = Color3.fromRGB(255, 255, 255)
        else
            if activePlayButton and activePlayButton ~= PlayPauseBtn then
                activePlayButton.Text = "▶"
                activePlayButton.TextColor3 = Color3.fromRGB(85, 255, 0)
                if activePlayButton.Parent and activePlayButton.Parent:FindFirstChild("MusicBox") then
                    activePlayButton.Parent.MusicBox.TextColor3 = Color3.fromRGB(255, 255, 255)
                end
            end

            if playingId ~= formattedId then
                currentSound:Stop()
                currentSound.SoundId = formattedId
            end

            currentSound:Play()
            playingId = formattedId
            activePlayButton = PlayPauseBtn

            PlayPauseBtn.Text = "⏸"
            PlayPauseBtn.TextColor3 = Color3.fromRGB(255, 200, 0)
            MusicBox.TextColor3 = Color3.fromRGB(85, 255, 0)
        end
    end)

    -- Evento Lixeira
    DeleteBtn.MouseButton1Click:Connect(function()
        if playingId == "rbxassetid://" .. songId then
            currentSound:Stop()
            playingId = ""
            activePlayButton = nil
        end

        for i, song in ipairs(savedSongs) do
            if song.id == songId and song.name == songName then
                table.remove(savedSongs, i)
                break
            end
        end

        ItemRow:Destroy()
        ScrollList.CanvasSize = UDim2.new(0, 0, 0, #savedSongs * 41)
    end)

    ScrollList.CanvasSize = UDim2.new(0, 0, 0, #savedSongs * 41)
end

-- Botão Adicionar
AddButton.MouseButton1Click:Connect(function()
    local id = IdInput.Text:gsub("%s+", "")
    local name = NameInput.Text

    if id ~= "" and name ~= "" then
        createMusicCard(name, id, false)
        IdInput.Text = ""
        NameInput.Text = ""
    end
end)

-- Botão Salvar
SaveButton.MouseButton1Click:Connect(function()
    if writefile then
        local success = pcall(function()
            writefile(FILE_PATH, HttpService:JSONEncode(savedSongs))
        end)
        if success then
            SaveButton.Text = "✅"
            task.wait(1)
            SaveButton.Text = "💾"
        end
    end
end)

-- Carregar Músicas Salvas
if isfile and isfile(FILE_PATH) and readfile then
    local success, result = pcall(function()
        return HttpService:JSONDecode(readfile(FILE_PATH))
    end)
    if success and type(result) == "table" then
        savedSongs = result
        for _, song in ipairs(savedSongs) do
            createMusicCard(song.name, song.id, true)
        end
    end
end

----------------------------------------------------
-- ABRIR E FECHAR
----------------------------------------------------
ToggleButton.MouseButton1Click:Connect(function()
    MainFrame.Visible = not MainFrame.Visible
end)

CloseButton.MouseButton1Click:Connect(function()
    MainFrame.Visible = false
end)
