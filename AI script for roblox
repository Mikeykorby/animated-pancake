-- Roblox Chatbot Script with Ollama (LLaMA 3.1) and Velocity Executor
-- Enhanced UI, supports both old 2017 chat and new TextChatService, memory for 30 messages, reopen button, smooth dragging, and dynamic prefix based on name format

-- MEMORY SETUP --
local memory = {}
local MAX_MEMORY = 30 -- Limit memory to 30 messages

-- Add the memory of the current conversation
local function addToMemory(message, response)
    if #memory >= MAX_MEMORY then
        table.remove(memory, 1) -- Remove the oldest entry if at limit
    end
    table.insert(memory, {message = message, response = response})
    warn("Memory updated. Current memory size: " .. #memory)
end

-- Reset memory function
local function resetMemory()
    memory = {}
    warn("Memory has been reset!")
end

local AI_ACTIVE = true  -- Flag to turn AI on and off
local CLOSE_RANGE_ONLY = true

_G.MESSAGE_SETTINGS = {
    ["MINIMUM_CHARACTERS"] = 1,
    ["MAXIMUM_CHARACTERS"] = 200,
    ["MAXIMUM_STUDS"] = 11,
}

_G.WHITELISTED = { -- Only works if CLOSE_RANGE_ONLY is disabled
    ["seem2006"] = true,
}

_G.BLACKLISTED = { -- Only works if CLOSE_RANGE_ONLY is enabled
    ["Builderman"] = true,
}

_G.PLAYER_NAME_FORMAT = "P" -- Default player name format (just 'P')
_G.NAME_SEPARATOR = ","  -- Default separator (can be comma or colon)

-- GUI SETUP --
local UserInputService = game:GetService("UserInputService")
local screenGui = Instance.new("ScreenGui")
screenGui.Name = "PersistentScreenGui"
screenGui.Parent = game.Players.LocalPlayer:WaitForChild("PlayerGui")
screenGui.ResetOnSpawn = false
screenGui.IgnoreGuiInset = true

-- Main Frame
local frame = Instance.new("Frame")
frame.Size = UDim2.new(0, 300, 0, 200)
frame.Position = UDim2.new(0.5, -150, 0.5, -100)
frame.BackgroundColor3 = Color3.fromRGB(30, 30, 30)
frame.BackgroundTransparency = 0.1
frame.BorderSizePixel = 0
frame.Parent = screenGui

-- Rounded Corners for Main Frame
local frameCorner = Instance.new("UICorner")
frameCorner.CornerRadius = UDim.new(0, 10)
frameCorner.Parent = frame

-- Title Label
local titleLabel = Instance.new("TextLabel")
titleLabel.Size = UDim2.new(1, 0, 0, 40)
titleLabel.Position = UDim2.new(0, 0, 0, 0)
titleLabel.BackgroundTransparency = 1
titleLabel.Text = "oLLama AI Chatbot"
titleLabel.TextColor3 = Color3.fromRGB(255, 255, 255)
titleLabel.Font = Enum.Font.GothamBold
titleLabel.TextSize = 20
titleLabel.Parent = frame

-- Status Label
local statusLabel = Instance.new("TextLabel")
statusLabel.Size = UDim2.new(1, 0, 0, 20)
statusLabel.Position = UDim2.new(0, 0, 0, 40)
statusLabel.BackgroundTransparency = 1
statusLabel.Text = "Status: Idle"
statusLabel.TextColor3 = Color3.fromRGB(150, 150, 150)
statusLabel.Font = Enum.Font.Gotham
statusLabel.TextSize = 14
statusLabel.Parent = frame

-- Toggle AI Button
local toggleButton = Instance.new("TextButton")
toggleButton.Size = UDim2.new(0, 200, 0, 40)
toggleButton.Position = UDim2.new(0.5, -100, 0.5, -20)
toggleButton.BackgroundColor3 = Color3.fromRGB(0, 120, 215)
toggleButton.TextColor3 = Color3.fromRGB(255, 255, 255)
toggleButton.Text = "Turn AI OFF"
toggleButton.Font = Enum.Font.Gotham
toggleButton.TextSize = 16
toggleButton.BorderSizePixel = 0
toggleButton.Parent = frame

local toggleButtonCorner = Instance.new("UICorner")
toggleButtonCorner.CornerRadius = UDim.new(0, 8)
toggleButtonCorner.Parent = toggleButton

-- Hover Effect for Toggle Button
toggleButton.MouseEnter:Connect(function()
    toggleButton.BackgroundColor3 = Color3.fromRGB(0, 150, 255)
end)
toggleButton.MouseLeave:Connect(function()
    toggleButton.BackgroundColor3 = Color3.fromRGB(0, 120, 215)
end)

-- Settings Button
local settingsButton = Instance.new("TextButton")
settingsButton.Size = UDim2.new(0, 200, 0, 40)
settingsButton.Position = UDim2.new(0.5, -100, 0.5, 30)
settingsButton.BackgroundColor3 = Color3.fromRGB(0, 120, 215)
settingsButton.TextColor3 = Color3.fromRGB(255, 255, 255)
settingsButton.Text = "Settings"
settingsButton.Font = Enum.Font.Gotham
settingsButton.TextSize = 16
settingsButton.BorderSizePixel = 0
settingsButton.Parent = frame

local settingsButtonCorner = Instance.new("UICorner")
settingsButtonCorner.CornerRadius = UDim.new(0, 8)
settingsButtonCorner.Parent = settingsButton

-- Hover Effect for Settings Button
settingsButton.MouseEnter:Connect(function()
    settingsButton.BackgroundColor3 = Color3.fromRGB(0, 150, 255)
end)
settingsButton.MouseLeave:Connect(function()
    settingsButton.BackgroundColor3 = Color3.fromRGB(0, 120, 215)
end)

-- Close Button
local closeButton = Instance.new("TextButton")
closeButton.Size = UDim2.new(0, 30, 0, 30)
closeButton.Position = UDim2.new(1, -40, 0, 5)
closeButton.BackgroundColor3 = Color3.fromRGB(255, 85, 85)
closeButton.TextColor3 = Color3.fromRGB(255, 255, 255)
closeButton.Text = "X"
closeButton.Font = Enum.Font.GothamBold
closeButton.TextSize = 16
closeButton.BorderSizePixel = 0
closeButton.Parent = frame

local closeButtonCorner = Instance.new("UICorner")
closeButtonCorner.CornerRadius = UDim.new(0, 8)
closeButtonCorner.Parent = closeButton

-- Hover Effect for Close Button
closeButton.MouseEnter:Connect(function()
    closeButton.BackgroundColor3 = Color3.fromRGB(255, 115, 115)
end)
closeButton.MouseLeave:Connect(function()
    closeButton.BackgroundColor3 = Color3.fromRGB(255, 85, 85)
end)

-- Reopen Button (Initially Hidden)
local reopenButton = Instance.new("TextButton")
reopenButton.Size = UDim2.new(0, 40, 0, 40)
reopenButton.Position = UDim2.new(0, 10, 0.5, -20)
reopenButton.BackgroundColor3 = Color3.fromRGB(0, 120, 215)
reopenButton.TextColor3 = Color3.fromRGB(255, 255, 255)
reopenButton.Text = ">"
reopenButton.Font = Enum.Font.GothamBold
reopenButton.TextSize = 20
reopenButton.BorderSizePixel = 0
reopenButton.Visible = false
reopenButton.Parent = screenGui

local reopenButtonCorner = Instance.new("UICorner")
reopenButtonCorner.CornerRadius = UDim.new(0, 8)
reopenButtonCorner.Parent = reopenButton

-- Hover Effect for Reopen Button
reopenButton.MouseEnter:Connect(function()
    reopenButton.BackgroundColor3 = Color3.fromRGB(0, 150, 255)
end)
reopenButton.MouseLeave:Connect(function()
    reopenButton.BackgroundColor3 = Color3.fromRGB(0, 120, 215)
end)

-- Settings Frame
local settingsFrame = Instance.new("Frame")
settingsFrame.Size = UDim2.new(0, 350, 0, 500)
settingsFrame.Position = UDim2.new(0.5, -175, 0.5, -250)
settingsFrame.BackgroundColor3 = Color3.fromRGB(30, 30, 30)
settingsFrame.BackgroundTransparency = 0.1
settingsFrame.BorderSizePixel = 0
settingsFrame.Visible = false
settingsFrame.Parent = screenGui

local settingsFrameCorner = Instance.new("UICorner")
settingsFrameCorner.CornerRadius = UDim.new(0, 10)
settingsFrameCorner.Parent = settingsFrame

-- Settings Title
local settingsTitle = Instance.new("TextLabel")
settingsTitle.Size = UDim2.new(1, 0, 0, 40)
settingsTitle.Position = UDim2.new(0, 0, 0, 0)
settingsTitle.BackgroundTransparency = 1
settingsTitle.Text = "Settings"
settingsTitle.TextColor3 = Color3.fromRGB(255, 255, 255)
settingsTitle.Font = Enum.Font.GothamBold
settingsTitle.TextSize = 20
settingsTitle.Parent = settingsFrame

-- AI Toggle Button (Settings)
local aiToggleButton = Instance.new("TextButton")
aiToggleButton.Size = UDim2.new(0, 250, 0, 40)
aiToggleButton.Position = UDim2.new(0.5, -125, 0, 60)
aiToggleButton.BackgroundColor3 = Color3.fromRGB(85, 170, 85)
aiToggleButton.TextColor3 = Color3.fromRGB(255, 255, 255)
aiToggleButton.Text = "Toggle AI"
aiToggleButton.Font = Enum.Font.Gotham
aiToggleButton.TextSize = 16
aiToggleButton.BorderSizePixel = 0
aiToggleButton.Parent = settingsFrame

local aiToggleButtonCorner = Instance.new("UICorner")
aiToggleButtonCorner.CornerRadius = UDim.new(0, 8)
aiToggleButtonCorner.Parent = aiToggleButton

-- Hover Effect for AI Toggle Button
aiToggleButton.MouseEnter:Connect(function()
    aiToggleButton.BackgroundColor3 = Color3.fromRGB(115, 200, 115)
end)
aiToggleButton.MouseLeave:Connect(function()
    aiToggleButton.BackgroundColor3 = Color3.fromRGB(85, 170, 85)
end)

-- Reset Memory Button
local resetButton = Instance.new("TextButton")
resetButton.Size = UDim2.new(0, 250, 0, 40)
resetButton.Position = UDim2.new(0.5, -125, 0, 110)
resetButton.BackgroundColor3 = Color3.fromRGB(255, 85, 85)
resetButton.TextColor3 = Color3.fromRGB(255, 255, 255)
resetButton.Text = "Reset Memory"
resetButton.Font = Enum.Font.Gotham
resetButton.TextSize = 16
resetButton.BorderSizePixel = 0
resetButton.Parent = settingsFrame

local resetButtonCorner = Instance.new("UICorner")
resetButtonCorner.CornerRadius = UDim.new(0, 8)
resetButtonCorner.Parent = resetButton

-- Hover Effect for Reset Button
resetButton.MouseEnter:Connect(function()
    resetButton.BackgroundColor3 = Color3.fromRGB(255, 115, 115)
end)
resetButton.MouseLeave:Connect(function()
    resetButton.BackgroundColor3 = Color3.fromRGB(255, 85, 85)
end)

-- TextBox to Customize Player Name Format
local nameFormatLabel = Instance.new("TextLabel")
nameFormatLabel.Size = UDim2.new(0, 250, 0, 20)
nameFormatLabel.Position = UDim2.new(0.5, -125, 0, 160)
nameFormatLabel.BackgroundTransparency = 1
nameFormatLabel.Text = "Player Name Format:"
nameFormatLabel.TextColor3 = Color3.fromRGB(200, 200, 200)
nameFormatLabel.Font = Enum.Font.Gotham
nameFormatLabel.TextSize = 14
nameFormatLabel.Parent = settingsFrame

local nameFormatInput = Instance.new("TextBox")
nameFormatInput.Size = UDim2.new(0, 250, 0, 40)
nameFormatInput.Position = UDim2.new(0.5, -125, 0, 180)
nameFormatInput.BackgroundColor3 = Color3.fromRGB(50, 50, 50)
nameFormatInput.TextColor3 = Color3.fromRGB(255, 255, 255)
nameFormatInput.Text = _G.PLAYER_NAME_FORMAT
nameFormatInput.Font = Enum.Font.Gotham
nameFormatInput.TextSize = 16
nameFormatInput.ClearTextOnFocus = false
nameFormatInput.BorderSizePixel = 0
nameFormatInput.Parent = settingsFrame

local nameFormatInputCorner = Instance.new("UICorner")
nameFormatInputCorner.CornerRadius = UDim.new(0, 8)
nameFormatInputCorner.Parent = nameFormatInput

-- Separator Dropdown
local separatorLabel = Instance.new("TextLabel")
separatorLabel.Size = UDim2.new(0, 250, 0, 20)
separatorLabel.Position = UDim2.new(0.5, -125, 0, 230)
separatorLabel.BackgroundTransparency = 1
separatorLabel.Text = "Name Separator:"
separatorLabel.TextColor3 = Color3.fromRGB(200, 200, 200)
separatorLabel.Font = Enum.Font.Gotham
separatorLabel.TextSize = 14
separatorLabel.Parent = settingsFrame

local separatorDropdown = Instance.new("TextButton")
separatorDropdown.Size = UDim2.new(0, 250, 0, 40)
separatorDropdown.Position = UDim2.new(0.5, -125, 0, 250)
separatorDropdown.BackgroundColor3 = Color3.fromRGB(50, 170, 50)
separatorDropdown.TextColor3 = Color3.fromRGB(255, 255, 255)
separatorDropdown.Text = "Select Separator: Comma"
separatorDropdown.Font = Enum.Font.Gotham
separatorDropdown.TextSize = 16
separatorDropdown.BorderSizePixel = 0
separatorDropdown.Parent = settingsFrame

local separatorDropdownCorner = Instance.new("UICorner")
separatorDropdownCorner.CornerRadius = UDim.new(0, 8)
separatorDropdownCorner.Parent = separatorDropdown

-- Hover Effect for Separator Dropdown
separatorDropdown.MouseEnter:Connect(function()
    separatorDropdown.BackgroundColor3 = Color3.fromRGB(80, 200, 80)
end)
separatorDropdown.MouseLeave:Connect(function()
    separatorDropdown.BackgroundColor3 = Color3.fromRGB(50, 170, 50)
end)

-- Toggle Name Prefix Button
local toggleNamePrefixButton = Instance.new("TextButton")
toggleNamePrefixButton.Size = UDim2.new(0, 250, 0, 40)
toggleNamePrefixButton.Position = UDim2.new(0.5, -125, 0, 300)
toggleNamePrefixButton.BackgroundColor3 = Color3.fromRGB(255, 170, 0)
toggleNamePrefixButton.TextColor3 = Color3.fromRGB(255, 255, 255)
toggleNamePrefixButton.Text = "Disable Name Prefix"
toggleNamePrefixButton.Font = Enum.Font.Gotham
toggleNamePrefixButton.TextSize = 16
toggleNamePrefixButton.BorderSizePixel = 0
toggleNamePrefixButton.Parent = settingsFrame

local toggleNamePrefixButtonCorner = Instance.new("UICorner")
toggleNamePrefixButtonCorner.CornerRadius = UDim.new(0, 8)
toggleNamePrefixButtonCorner.Parent = toggleNamePrefixButton

-- Hover Effect for Toggle Name Prefix Button
toggleNamePrefixButton.MouseEnter:Connect(function()
    toggleNamePrefixButton.BackgroundColor3 = Color3.fromRGB(255, 200, 50)
end)
toggleNamePrefixButton.MouseLeave:Connect(function()
    toggleNamePrefixButton.BackgroundColor3 = Color3.fromRGB(255, 170, 0)
end)

-- Memory Limit Label and TextBox
local memoryLimitLabel = Instance.new("TextLabel")
memoryLimitLabel.Size = UDim2.new(0, 250, 0, 20)
memoryLimitLabel.Position = UDim2.new(0.5, -125, 0, 350)
memoryLimitLabel.BackgroundTransparency = 1
memoryLimitLabel.Text = "memory limit"
memoryLimitLabel.TextColor3 = Color3.fromRGB(200, 200, 200)
memoryLimitLabel.Font = Enum.Font.Gotham
memoryLimitLabel.TextSize = 14
memoryLimitLabel.Parent = settingsFrame

local memoryLimitInput = Instance.new("TextBox")
memoryLimitInput.Size = UDim2.new(0, 250, 0, 40)
memoryLimitInput.Position = UDim2.new(0.5, -125, 0, 370)
memoryLimitInput.BackgroundColor3 = Color3.fromRGB(50, 50, 50)
memoryLimitInput.TextColor3 = Color3.fromRGB(255, 255, 255)
memoryLimitInput.Text = tostring(MAX_MEMORY)
memoryLimitInput.Font = Enum.Font.Gotham
memoryLimitInput.TextSize = 16
memoryLimitInput.ClearTextOnFocus = false
memoryLimitInput.BorderSizePixel = 0
memoryLimitInput.Parent = settingsFrame

local memoryLimitInputCorner = Instance.new("UICorner")
memoryLimitInputCorner.CornerRadius = UDim.new(0, 8)
memoryLimitInputCorner.Parent = memoryLimitInput

-- Update MAX_MEMORY when focus is lost
memoryLimitInput.FocusLost:Connect(function()
    local newLimit = tonumber(memoryLimitInput.Text) or 30
    MAX_MEMORY = math.clamp(newLimit, 1, 100) -- Limit between 1 and 100
    memoryLimitInput.Text = tostring(MAX_MEMORY)
    warn("Memory limit updated to: " .. MAX_MEMORY)
end)

-- SMOOTH DRAGGING FUNCTIONALITY --
local function makeDraggable(frame)
    local dragging = false
    local dragStart, startPos

    UserInputService.InputBegan:Connect(function(input, gameProcessed)
        if gameProcessed then return end
        if input.UserInputType == Enum.UserInputType.MouseButton1 or input.UserInputType == Enum.UserInputType.Touch then
            local position = input.Position
            local guiPosition = frame.Position
            local guiSize = frame.Size
            local guiX = guiPosition.X.Scale * game:GetService("GuiService"):GetScreenResolution().X + guiPosition.X.Offset
            local guiY = guiPosition.Y.Scale * game:GetService("GuiService"):GetScreenResolution().Y + guiPosition.Y.Offset
            local guiWidth = guiSize.X.Scale * game:GetService("GuiService"):GetScreenResolution().X + guiSize.X.Offset
            local guiHeight = guiSize.Y.Scale * game:GetService("GuiService"):GetScreenResolution().Y + guiSize.Y.Offset

            if position.X >= guiX and position.X <= guiX + guiWidth and position.Y >= guiY and position.Y <= guiY + guiHeight then
                dragging = true
                dragStart = position
                startPos = frame.Position
            end
        end
    end)

    UserInputService.InputEnded:Connect(function(input)
        if input.UserInputType == Enum.UserInputType.MouseButton1 or input.UserInputType == Enum.UserInputType.Touch then
            dragging = false
        end
    end)

    UserInputService.InputChanged:Connect(function(input)
        if dragging and (input.UserInputType == Enum.UserInputType.MouseMovement or input.UserInputType == Enum.UserInputType.Touch) then
            local delta = input.Position - dragStart
            local newX = startPos.X.Offset + delta.X
            local newY = startPos.Y.Offset + delta.Y
            frame.Position = UDim2.new(startPos.X.Scale, newX, startPos.Y.Scale, newY)
        end
    end)
end

-- Apply smooth dragging to both frames
makeDraggable(frame)
makeDraggable(settingsFrame)

-- SETTINGS HANDLERS --
local function toggleFrameVisibility()
    settingsFrame.Visible = not settingsFrame.Visible
end

local function toggleAI()
    AI_ACTIVE = not AI_ACTIVE
    toggleButton.Text = AI_ACTIVE and "Turn AI OFF" or "Turn AI ON"
    statusLabel.Text = AI_ACTIVE and "Status: Active" or "Status: Inactive"
end

settingsButton.MouseButton1Click:Connect(function()
    toggleFrameVisibility()
end)

closeButton.MouseButton1Click:Connect(function()
    frame.Visible = false
    settingsFrame.Visible = false
    reopenButton.Visible = true
end)

reopenButton.MouseButton1Click:Connect(function()
    frame.Visible = true
    reopenButton.Visible = false
    frame.Position = UDim2.new(0.5, -150, 0.5, -100) -- Reset position to center
end)

aiToggleButton.MouseButton1Click:Connect(function()
    toggleAI()
end)

resetButton.MouseButton1Click:Connect(function()
    _G.PLAYER_NAME_FORMAT = "P"
    nameFormatInput.Text = _G.PLAYER_NAME_FORMAT
    resetMemory()
end)

-- Change the player name format dynamically --
nameFormatInput.FocusLost:Connect(function()
    _G.PLAYER_NAME_FORMAT = nameFormatInput.Text
    warn("Player name format updated to: " .. _G.PLAYER_NAME_FORMAT)
end)

-- Handle Separator Dropdown for Comma or Colon --
separatorDropdown.MouseButton1Click:Connect(function()
    _G.NAME_SEPARATOR = (_G.NAME_SEPARATOR == ",") and ":" or ","
    separatorDropdown.Text = "Select Separator: " .. (_G.NAME_SEPARATOR == "," and "Comma" or "Colon")
    warn("Separator updated to: " .. _G.NAME_SEPARATOR)
end)

-- Toggle Player Name Prefix --
toggleNamePrefixButton.MouseButton1Click:Connect(function()
    if _G.PLAYER_NAME_FORMAT == "P" then
        _G.PLAYER_NAME_FORMAT = ""
        toggleNamePrefixButton.Text = "Enable Name Prefix"
    else
        _G.PLAYER_NAME_FORMAT = "P"
        toggleNamePrefixButton.Text = "Disable Name Prefix"
    end
    nameFormatInput.Text = _G.PLAYER_NAME_FORMAT
    warn("Player name prefix toggled to: " .. (_G.PLAYER_NAME_FORMAT == "" and "Disabled" or "Enabled"))
end)

-- AI RESPONSE HANDLING --
local chat = function(_string)
    warn("Attempting to send message: " .. _string)
    if game.TextChatService.ChatVersion == Enum.ChatVersion.TextChatService then
        print("FIRING ".._string.."...")
        local success, err = pcall(function()
            game.TextChatService.TextChannels.RBXGeneral:SendAsync(_string, "All")
        end)
        if not success then
            warn("Failed to send message via TextChatService: "..err)
        else
            warn("FIRED via TextChatService!")
        end
    else
        local success, err = pcall(function()
            game:GetService('ReplicatedStorage').DefaultChatSystemChatEvents.SayMessageRequest:FireServer(_string, 'All')
        end)
        if not success then
            warn("Failed to send message via legacy chat: "..err)
        else
            warn("FIRED via legacy chat!")
        end
    end
end

-- Handling chat messages and responses --
local TextChatService = game:GetService("TextChatService")
local ReplicatedStorage = game:GetService("ReplicatedStorage")
local Players = game:GetService("Players")
local HttpService = game:GetService("HttpService")
local LocalPlayer = Players.LocalPlayer
local Debounce = false

local RequestFunction = syn and syn.request or request

local function MakeRequest(Prompt)
    return RequestFunction({
        Url = "http://localhost:11434/api/generate",
        Method = "POST",
        Headers = {
            ["Content-Type"] = "application/json"
        },
        Body = game:GetService("HttpService"):JSONEncode({
            model = "llama3.1", 
            prompt = Prompt,
            stream = false
        })
    })
end

-- Function to process messages (shared between both chat systems)
local function processMessage(Message, player, Character)
    warn("Processing message from " .. player.Name .. ": " .. Message)
    if not AI_ACTIVE then
        warn("AI is not active, skipping message.")
        return
    end
    if player == LocalPlayer then
        warn("Message from local player, skipping.")
        return
    end
    if string.match(Message, "#") then
        warn("Message contains '#', skipping.")
        return
    end
    if not Character or not Character:FindFirstChild("Head") then
        warn("Player character or head not found, skipping.")
        return
    end
    if not LocalPlayer.Character or not LocalPlayer.Character:FindFirstChild("Head") then
        warn("Local player character or head not found, skipping.")
        return
    end
    if Debounce then
        warn("Debounce active, skipping.")
        return
    end
    if #Message < _G.MESSAGE_SETTINGS["MINIMUM_CHARACTERS"] or #Message > _G.MESSAGE_SETTINGS["MAXIMUM_CHARACTERS"] then
        warn("Message length out of bounds (" .. #Message .. "), skipping.")
        return
    end
    if CLOSE_RANGE_ONLY then 
        if _G.BLACKLISTED[player.Name] then
            warn("Player " .. player.Name .. " is blacklisted, skipping.")
            return
        end
        if (Character.Head.Position - LocalPlayer.Character.Head.Position).Magnitude > _G.MESSAGE_SETTINGS["MAXIMUM_STUDS"] then
            warn("Player " .. player.Name .. " is too far (" .. (Character.Head.Position - LocalPlayer.Character.Head.Position).Magnitude .. " studs), skipping.")
            return
        end
    elseif not _G.WHITELISTED[player.Name] then
        warn("Player " .. player.Name .. " is not whitelisted, skipping.")
        return
    end

    Debounce = true
    statusLabel.Text = "Status: Processing..."

    local Response = ""
    if string.lower(Message) == "what did i just say" and #memory > 0 then
        -- Directly recall the last message from memory
        Response = "You just said: " .. memory[#memory].message
    else
        -- Proceed with Ollama request, including last message for context
        local context = #memory > 0 and "Last message: " .. memory[#memory].message .. ". Current message: " .. Message or Message
        local Prompt = "(note: dont use any line breaks and keep the messages shorter) " .. context
        local HttpRequest = MakeRequest(Prompt)
        print("["..player.Name.."]: "..Message)
        if HttpRequest.StatusCode == 200 then
            local responseData = game:GetService("HttpService"):JSONDecode(HttpRequest.Body)
            local actualResponse = responseData.response

            if actualResponse == nil then
                warn("fix your script: response is nil")
                Response = "Sorry, I couldn't respond. Try again!"
            else 
                -- Dynamically set the prefix based on _G.PLAYER_NAME_FORMAT
                local prefix = ""
                if _G.PLAYER_NAME_FORMAT == "ollama" then
                    prefix = "[oLLama AI] " .. player.Name .. _G.NAME_SEPARATOR .. " "
                elseif _G.PLAYER_NAME_FORMAT == "P" then
                    prefix = player.Name .. _G.NAME_SEPARATOR .. " "
                elseif _G.PLAYER_NAME_FORMAT == "" then
                    prefix = "" -- No prefix if the name format is empty
                else
                    prefix = _G.PLAYER_NAME_FORMAT .. " " .. player.Name .. _G.NAME_SEPARATOR .. " "
                end
                Response = prefix .. actualResponse
                warn("Sending: "..Response)
            end
        else
            warn("Request failed with status code: " .. HttpRequest.StatusCode)
            Response = "Sorry, I couldn't respond. Try again!"
        end
    end

    -- Add to memory before sending response
    addToMemory(Message, string.match(Response, "^%[.-%] .-: (.*)") or Response)

    chat(string.sub(Response, 1, 128))
    if #Response > 128 then
        delay(1, function()
            chat(string.sub(Response, 129))
        end)
    end
    wait()
    statusLabel.Text = AI_ACTIVE and "Status: Active" or "Status: Inactive"
    Debounce = false
end

-- Detect messages using TextChatService (new chat system)
if TextChatService.ChatVersion == Enum.ChatVersion.TextChatService then
    local channel = TextChatService.TextChannels.RBXGeneral
    if not channel then
        warn("RBXGeneral channel not found. Attempting to find another channel...")
        for _, chan in pairs(TextChatService.TextChannels:GetChildren()) do
            if chan:IsA("TextChannel") then
                channel = chan
                warn("Found channel: " .. chan.Name)
                break
            end
        end
    end
    if channel then
        warn("Listening for messages on channel: " .. channel.Name)
        channel.MessageReceived:Connect(function(message)
            warn("Message received via TextChatService: " .. message.Text)
            local sender = message.TextSource
            if not sender then
                warn("No sender found for message.")
                return
            end
            local player = Players:GetPlayerByUserId(sender.UserId)
            if not player then
                warn("No player found for sender ID: " .. sender.UserId)
                return
            end
            local Message = message.Text
            local Character = player.Character
            processMessage(Message, player, Character)
        end)
    else
        warn("No TextChatService channel found. New chat system will not work.")
    end
end

-- Detect messages using legacy chat system (2017 chat)
local success, err = pcall(function()
    local OnMessageDoneFiltering = ReplicatedStorage:WaitForChild("DefaultChatSystemChatEvents", 5):WaitForChild("OnMessageDoneFiltering", 5)
    warn("Legacy chat system found, setting up listener...")
    OnMessageDoneFiltering.OnClientEvent:Connect(function(Table)
        warn("Message received via legacy chat: " .. Table.Message)
        local Message, Instance = Table.Message, Players:FindFirstChild(Table.FromSpeaker)
        local Character = Instance and Instance.Character
        processMessage(Message, Instance, Character)
    end)
end)
if not success then
    warn("Failed to set up legacy chat listener: " .. err)
end

-- Test Ollama connection on startup
local testRequest = MakeRequest("Test connection")
if testRequest.StatusCode == 200 then
    warn("Ollama connection successful!")
else
    warn("Ollama connection failed with status code: " .. testRequest.StatusCode)
end

-- Send initial message with delay to ensure chat system is ready
warn("Script has been executed with success.")
delay(2, function()
    chat("LLaMA 3.1 Model Loaded!")
end)
