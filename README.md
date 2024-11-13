local player = game.Players.LocalPlayer
local character = player.Character or player.CharacterAdded:Wait()
character:MoveTo(Vector3.new(-2533, 50, 5159))

wait(1)
for i = 1, 1000 do
    local args = {
        [1] = "RevivePlayerEr",
        [2] = game:GetService("Players").LocalPlayer
    }

    game:GetService("ReplicatedStorage"):WaitForChild("ReviveSystem"):WaitForChild("Event"):FireServer(unpack(args))
end
