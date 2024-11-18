local Fluent = loadstring(game:HttpGet("https://github.com/dawid-scripts/Fluent/releases/latest/download/main.lua"))()
local SaveManager = loadstring(game:HttpGet("https://raw.githubusercontent.com/dawid-scripts/Fluent/master/Addons/SaveManager.lua"))()
local InterfaceManager = loadstring(game:HttpGet("https://raw.githubusercontent.com/dawid-scripts/Fluent/master/Addons/InterfaceManager.lua"))()

local Window = Fluent:CreateWindow({
    Title = "Fluent " .. Fluent.Version,
    SubTitle = "by dawid",
    TabWidth = 160,
    Size = UDim2.fromOffset(580, 460),
    Acrylic = true, -- The blur may be detectable, setting this to false disables blur entirely
    Theme = "Dark",
    MinimizeKey = Enum.KeyCode.LeftControl -- Used when theres no MinimizeKeybind
})

--Fluent provides Lucide Icons https://lucide.dev/icons/ for the tabs, icons are optional
local Tabs = {
    Main = Window:AddTab({ Title = "Main", Icon = "" }),
    Settings = Window:AddTab({ Title = "Settings", Icon = "settings" })
}

local Options = Fluent.Options

do
    Fluent:Notify({
        Title = "Notification",
        Content = "This is a notification",
        SubContent = "SubContent", -- Optional
        Duration = 5 -- Set to nil to make the notification not disappear
    })



    Tabs.Main:AddParagraph({
        Title = "Paragraph",
        Content = "This is a paragraph.\nSecond line!"
    })



    Tabs.Main:AddButton({
        Title = "KnucklesUpgrade Level 1-5",
        Description = "Very important button",
        Callback = function()
            Window:Dialog({
                Title = "Title",
                Content = "This is a dialog",
                Buttons = {
                    {
                        Title = "Confirm",
                        Callback = function()
local UserInputService = game:GetService("UserInputService")
local Player = game:GetService("Players").LocalPlayer
local Character = Player.Character

-- ฟังก์ชันสำหรับยิงคำสั่งรัว
local function fireKnuckles()
    local upgradeLevels = {5, 4, 3, 2, 1, 0} -- ระดับของ KnucklesUpgrade
    for _, level in ipairs(upgradeLevels) do
        local upgradeName = level > 0 and ("KnucklesUpgrade" .. level) or "KnucklesUpgrade"
        local upgrade = Character:FindFirstChild(upgradeName)

        if upgrade and upgrade:FindFirstChild("Handle") and upgrade:FindFirstChild("Combo") and upgrade.Combo:FindFirstChild("C2") then
            local args = { [1] = upgrade.Handle }
            upgrade.Combo.C2:FireServer(unpack(args))
            task.wait(0.1) -- รอ 0.1 วินาทีก่อนคำสั่งถัดไป
        end
    end
end

-- ตรวจจับการกดปุ่ม Q
UserInputService.InputBegan:Connect(function(input, gameProcessed)
    if gameProcessed then return end -- หลีกเลี่ยงการทำงานซ้ำซ้อนหากเกมจัดการคำสั่งแล้ว

    if input.KeyCode == Enum.KeyCode.Q then
        fireKnuckles() -- เรียกฟังก์ชันยิงรัว
    end
end)




                        end
                    },
                    {
                        Title = "Cancel",
                        Callback = function()
                            print("Cancelled the dialog.")
                        end
                    }
                }
            })
        end
    })
    


        Tabs.Main:AddButton({
        Title = "Pool_RedUpgrade Level 1-5",
        Description = "Very important button",
        Callback = function()
            Window:Dialog({
                Title = "Title",
                Content = "This is a dialog",
                Buttons = {
                    {
                        Title = "Confirm",
                        Callback = function()
                     local UserInputService = game:GetService("UserInputService")

-- ตรวจสอบเมื่อกดปุ่ม Q
UserInputService.InputBegan:Connect(function(input, gameProcessedEvent)
    if gameProcessedEvent then return end  -- หลีกเลี่ยงการทำงานถ้าเกมกำลังจัดการกับป้อนข้อมูล

    if input.UserInputType == Enum.UserInputType.Keyboard and input.KeyCode == Enum.KeyCode.Q then
        -- ใช้ loop เพื่อจัดการ Pool_RedUpgrade
        for i = 5, 0, -1 do
            local upgradeName = i > 0 and ("Pool_RedUpgrade" .. i) or "Pool_RedUpgrade"
            local character = game:GetService("Players").LocalPlayer.Character
            local handle = character:FindFirstChild(upgradeName) and character[upgradeName]:FindFirstChild("Handle")
            local combo = character:FindFirstChild(upgradeName) and character[upgradeName]:FindFirstChild("Combo")

            if handle and combo and combo:FindFirstChild("Kie") then
                local args = { [1] = handle }
                combo.Kie:FireServer(unpack(args))
            end
        end
    end
end)





                        end
                    },
                    {
                        Title = "Cancel",
                        Callback = function()
                            print("Cancelled the dialog.")
                        end
                    }
                }
            })
        end
    })
Tabs.Main:AddButton({
        Title = "Bat_RedUpgrade Level 1-5",
        Description = "Very important button",
        Callback = function()
            Window:Dialog({
                Title = "Title",
                Content = "This is a dialog",
                Buttons = {
                    {
                        Title = "Confirm",
                        Callback = function()
                local UserInputService = game:GetService("UserInputService")

-- ตรวจสอบเมื่อกดปุ่ม Q
UserInputService.InputBegan:Connect(function(input, gameProcessedEvent)
    if gameProcessedEvent then return end  -- หลีกเลี่ยงการทำงานถ้าเกมกำลังจัดการกับป้อนข้อมูล

    if input.UserInputType == Enum.UserInputType.Keyboard and input.KeyCode == Enum.KeyCode.Q then
        -- รันคำสั่ง FireServer สำหรับทุก Bat_RedUpgrade
        for i = 5, 0, -1 do
            local UpgradeUpgradeName = i > 0 and ("Bat_RedUpgrade" .. i) or "Bat_RedUpgrade"
            local character = game:GetService("Players").LocalPlayer.Character
            local handle = character:FindFirstChild(UpgradeName) and character[UpgradeName]:FindFirstChild("Handle")
            local combo = character:FindFirstChild(UpgradeName) and character[UpgradeName]:FindFirstChild("Combo")

            if handle and combo and combo:FindFirstChild("Kie") then
                local args = { [1] = handle }
                combo.Kie:FireServer(unpack(args))
            end
        end
    end
end)




                        end
                    },
                    {
                        Title = "Cancel",
                        Callback = function()
                            print("Cancelled the dialog.")
                        end
                    }
                }
            })
        end
    })
     end

    Tabs.Main:AddButton({
        Title = "Broken_BottleUpgrade Level 1-5",
        Description = "Very important button",
        Callback = function()
            Window:Dialog({
                Title = "Title",
                Content = "This is a dialog",
                Buttons = {
                    {
                        Title = "Confirm",
                        Callback = function()
                     local UserInputService = game:GetService("UserInputService")

-- ตรวจสอบเมื่อกดปุ่ม Q
UserInputService.InputBegan:Connect(function(input, gameProcessedEvent)
    if gameProcessedEvent then return end  -- หลีกเลี่ยงการทำงานถ้าเกมกำลังจัดการกับป้อนข้อมูล

    if input.UserInputType == Enum.UserInputType.Keyboard and input.KeyCode == Enum.KeyCode.Q then
        local character = game:GetService("Players").LocalPlayer.Character
        
        -- ใช้ loop เพื่อเรียกใช้ FireServer
        for i = 5, 0, -1 do
            local upgradeName = i > 0 and ("Broken_BottleUpgrade" .. i) or "Broken_BottleUpgrade"
            local handle = character:FindFirstChild(upgradeName) and character[upgradeName]:FindFirstChild("Handle")
            local combo = character:FindFirstChild(upgradeName) and character[upgradeName]:FindFirstChild("Combo")

            if handle and combo and combo:FindFirstChild("Emo") then
                local args = { [1] = handle }
                combo.Emo:FireServer(unpack(args))
            end
        end
    end
end)





                        end
                    },
                    {
                        Title = "Cancel",
                        Callback = function()
                            print("Cancelled the dialog.")
                        end
                    }
                }
            })
        end
    })

        Tabs.Main:AddButton({
        Title = "M9Upgrade Level 1-5",
        Description = "Very important button",
        Callback = function()
            Window:Dialog({
                Title = "Title",
                Content = "This is a dialog",
                Buttons = {
                    {
                        Title = "Confirm",
                        Callback = function()
                                local UserInputService = game:GetService("UserInputService")

-- ตรวจสอบเมื่อกดปุ่ม Q
UserInputService.InputBegan:Connect(function(input, gameProcessedEvent)
    if gameProcessedEvent then return end  -- หลีกเลี่ยงการทำงานถ้าเกมกำลังจัดการกับป้อนข้อมูล

    if input.UserInputType == Enum.UserInputType.Keyboard and input.KeyCode == Enum.KeyCode.Q then
        -- รันคำสั่ง FireServer สำหรับทุก M9Upgrade
        for i = 5, 0, -1 do
            local UpgradeUpgradeName = i > 0 and ("M9Upgrade" .. i) or "M9Upgrade"
            local character = game:GetService("Players").LocalPlayer.Character
            local handle = character:FindFirstChild(UpgradeName) and character[UpgradeName]:FindFirstChild("Handle")
            local combo = character:FindFirstChild(UpgradeName) and character[UpgradeName]:FindFirstChild("Combo")

            if handle and combo and combo:FindFirstChild("Kie") then
                local args = { [1] = handle }
                combo.Kie:FireServer(unpack(args))
            end
        end
    end
end)





                        end
                    },
                    {
                        Title = "Cancel",
                        Callback = function()
                            print("Cancelled the dialog.")
                        end
                    }
                }
            })
        end
    })
    Tabs.Main:AddButton({
        Title = "MacheteUpgrade Level 1-5",
        Description = "Very important button",
        Callback = function()
            Window:Dialog({
                Title = "Title",
                Content = "This is a dialog",
                Buttons = {
                    {
                        Title = "Confirm",
                        Callback = function()
                     local UserInputService = game:GetService("UserInputService")

-- ตรวจสอบเมื่อกดปุ่ม Q
UserInputService.InputBegan:Connect(function(input, gameProcessedEvent)
    if gameProcessedEvent then return end  -- หลีกเลี่ยงการทำงานถ้าเกมกำลังจัดการกับป้อนข้อมูล

    if input.UserInputType == Enum.UserInputType.Keyboard and input.KeyCode == Enum.KeyCode.Q then
        local character = game:GetService("Players").LocalPlayer.Character
        
        -- ใช้ loop เพื่อเรียกใช้ FireServer
        for i = 5, 0, -1 do
            local upgradeName = i > 0 and ("MacheteUpgrade" .. i) or "MacheteUpgrade"
            local handle = character:FindFirstChild(upgradeName) and character[upgradeName]:FindFirstChild("Handle")
            local combo = character:FindFirstChild(upgradeName) and character[upgradeName]:FindFirstChild("Combo")

            if handle and combo and combo:FindFirstChild("Emo") then
                local args = { [1] = handle }
                combo.Emo:FireServer(unpack(args))
            end
        end
    end
end)





                        end
                    },
                    {
                        Title = "Cancel",
                        Callback = function()
                            print("Cancelled the dialog.")
                        end
                    }
                }
            })
        end
    })
