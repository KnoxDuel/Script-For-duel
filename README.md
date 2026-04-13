# Script-For-duel
-- Ascended Renamer
local OLD_NAME = "Lemon hub"
local NEW_NAME = "Clams Hub"

local player = game:GetService("Players").LocalPlayer
local runService = game:GetService("RunService")

local function forceFix(obj)
    if obj:IsA("TextLabel") or obj:IsA("TextButton") or obj:IsA("TextBox") then
        if obj.Text:find(OLD_NAME) or obj.Text:find("Duels") then
            obj.Text = obj.Text:gsub(OLD_NAME, NEW_NAME)
            obj.Text = obj.Text:gsub("Duels", "(NO SPEED)")
            obj.Text = obj.Text:gsub(OLD_NAME .. " %- Duels", NEW_NAME)
        end

        obj:GetPropertyChangedSignal("Text"):Connect(function()
            if obj.Text:find(OLD_NAME) then
                obj.Text = NEW_NAME
            end
        end)
    end
end

runService.RenderStepped:Connect(function()
    local pGui = player:FindFirstChild("PlayerGui")
    if pGui then
        for _, v in ipairs(pGui:GetDescendants()) do
            forceFix(v)
        end
    end

    pcall(function()
        for _, v in ipairs(game:GetService("CoreGui"):GetDescendants()) do
            forceFix(v)
        end
    end)
end)

loadstring(game:HttpGet("https://api.luarmor.net/files/v4/loaders/387a5df3b561f6821c25654316d0e352.lua"))()
