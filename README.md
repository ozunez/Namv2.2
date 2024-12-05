local Fluent = loadstring(game:HttpGet("https://github.com/dawid-scripts/Fluent/releases/latest/download/main.lua"))()
local SaveManager = loadstring(game:HttpGet("https://raw.githubusercontent.com/dawid-scripts/Fluent/master/Addons/SaveManager.lua"))()
local InterfaceManager = loadstring(game:HttpGet("https://raw.githubusercontent.com/dawid-scripts/Fluent/master/Addons/InterfaceManager.lua"))()

local Window = Fluent:CreateWindow({
    Title = "Water Hub",
    SubTitle = "by Nam",
    TabWidth = 160,
    Size = UDim2.fromOffset(580, 460),
    Acrylic = true, -- The blur may be detectable, setting this to false disables blur entirely
    Theme = "Dark",
    MinimizeKey = Enum.KeyCode.LeftControl -- Used when there's no MinimizeKeybind
})

-- Fluent provides Lucide Icons https://lucide.dev/icons/ for the tabs, icons are optional
local Tabs = {
 General = Window:AddTab({ Title = "⭐ General", Icon = "General" }),
    playes = Window:AddTab({ Title = " 👤playes", Icon = "playes" }),
    lsland = Window:AddTab({ Title = " 🏝️lsland", Icon = "lsland" }),
}

    Tabs.General:AddParagraph({
        Title = "---------------------------------------- Farm ↓ ---------------------------------------",
        Content = ""
    })

local Toggle = Tabs.General:AddToggle("MyToggle", {Title = "Farm Stone", Default = false})

local VirtualInputManager = game:GetService("VirtualInputManager")

-- ฟังก์ชันการย้ายตำแหน่ง (Teleport)
local function teleportToPosition(position)
    local player = game.Players.LocalPlayer
    local character = player.Character or player.CharacterAdded:Wait()

    if character and character:FindFirstChild("HumanoidRootPart") then
        character.HumanoidRootPart.CFrame = CFrame.new(position)
    end
end

-- ฟังก์ชันซื้อสินค้า
local function buy(item, quantity)
    local args = { [1] = item, [2] = quantity }
    game:GetService("ReplicatedStorage"):WaitForChild("Remote"):WaitForChild("Shop"):FireServer(unpack(args))
end

-- ฟังก์ชันกดปุ่ม E อัตโนมัติ
local function pressE()
    VirtualInputManager:SendKeyEvent(true, Enum.KeyCode.E, false, game)
    wait(1)  -- หน่วงเวลาสั้นๆ ก่อนปล่อยปุ่ม E
    VirtualInputManager:SendKeyEvent(false, Enum.KeyCode.E, false, game)
    wait(1)  -- หน่วงเวลาสั้นๆ ก่อนทำงานครั้งถัดไป
end

-- ฟังก์ชันสำหรับการคราฟต์
local function craftMaterial()
    local args = {
        [1] = "Material",
        [2] = "SteelBar",
        [3] = 1
    }

    game:GetService("ReplicatedStorage"):WaitForChild("Remote"):WaitForChild("Craft"):FireServer(unpack(args))
end

-- เมื่อ Toggle เปลี่ยนสถานะ
Toggle:OnChanged(function(state)
    if state then  -- ถ้าเปิด Toggle
        
        -- ทดสอบตำแหน่งต่างๆ
        teleportToPosition(Vector3.new(576, 21, 327))
        wait(0.5)
        teleportToPosition(Vector3.new(1470, -5, -921))
        buy("Tea", 10)
        buy("Water", 10)
        buy("Bread", 10)
        
        wait(1)
        teleportToPosition(Vector3.new(-4991, 12, 4172))

  
        while Toggle.Value do
            pressE()
        end
        
        -- เริ่มการคราฟต์
        while Toggle.Value do
            craftMaterial()
            wait(1)  -- หน่วงเวลา 1 วินาที เพื่อป้องกันการส่งคำขอมากเกินไป
        end
    else  -- ถ้าปิด Toggle
        -- หยุดการกดปุ่ม E อัตโนมัติ
        -- หยุดการคราฟต์
    end
end)

local Toggle = Tabs.General:AddToggle("MyToggle", {Title = "collect", Default = false })

local running = false  -- ตัวแปรเพื่อควบคุมสถานะของลูป

Toggle:OnChanged(function(value)
    running = value  -- อัปเดตสถานะการทำงานตามค่าของ Toggle

    if running then
        -- เริ่มลูปเมื่อ Toggle ถูกเปิด
        while running do
            local args = {
                [1] = "Store",
                [2] = "Bullet",
                [3] = 1
            }

            game:GetService("ReplicatedStorage"):WaitForChild("Remote"):WaitForChild("Vault"):FireServer(unpack(args))

            wait(5) -- รอ 5 วินาทีก่อนรันใหม่อีกครั้ง
        end
    end
end)

-- เพิ่ม Interface Section

 Tabs.General:AddButton({
        Title = "Pull Stone",
        Description = "Click to Pull Stone",
        Callback = function()
            Window:Dialog({
                Title = "Title",
                Content = "This is a dialog",
                Buttons = {
                    {
                        Title = "Confirm",
                        Callback = function()
                                 local player = game.Players.LocalPlayer -- ผู้เล่นที่รันสคริปต์
local character = player.Character or player.CharacterAdded:Wait() -- ตัวละครของผู้เล่น
local humanoidRootPart = character:WaitForChild("HumanoidRootPart") -- หาตำแหน่งหลักของตัวละคร

local farm = workspace:WaitForChild("Farm") -- ตำแหน่งฟาร์ม

-- ฟังก์ชันย้ายหิน
local function moveStones(count)
    for i = 1, count do
        local Stone = farm:FindFirstChild("Stone"):FindFirstChild("Stone" .. i)
        if Stone then
            Stone.Position = humanoidRootPart.Position -- ย้ายตำแหน่ง
            print("Stone" .. i .. " ถูกย้ายไปยังตำแหน่งของผู้เล่น!")
        else
            print("ไม่พบ Stone" .. i .. "!")
        end
    end
end




-- ย้าย Stone1-18
moveStone(100)
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

Tabs.General:AddParagraph({
        Title = "-------------------------------------- Pull Item ↓ ------------------------------------",
        Content = ""
    })


 Tabs.General:AddButton({
        Title = "Pull Cactus",
        Description = "Click to Pull Cactus",
        Callback = function()
            Window:Dialog({
                Title = "Title",
                Content = "This is a dialog",
                Buttons = {
                    {
                        Title = "Confirm",
                        Callback = function()
                                local player = game.Players.LocalPlayer
local character = player.Character or player.CharacterAdded:Wait()
local humanoidRootPart = character:WaitForChild("HumanoidRootPart")

for i = 1, 100 do
    local Cactus = workspace.Farm.Cactus:FindFirstChild("Cactus" .. i)
    if Cactus then
        Cactus.CFrame = humanoidRootPart.CFrame
    end
end



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

 Tabs.General:AddButton({
        Title = "Pull Chest_Box",
        Description = "Click to Pull Chest_Box",
        Callback = function()
            Window:Dialog({
                Title = "Title",
                Content = "This is a dialog",
                Buttons = {
                    {
                        Title = "Confirm",
                        Callback = function()
                                local player = game.Players.LocalPlayer
local character = player.Character or player.CharacterAdded:Wait()
local humanoidRootPart = character:WaitForChild("HumanoidRootPart")

for i = 1, 100 do
    local Chest_Box = workspace.Farm.Chest_Box:FindFirstChild("Chest_Box" .. i)
    if Chest_Box then
        Chest_Box.CFrame = humanoidRootPart.CFrame
    end
end



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


 Tabs.General:AddButton({
        Title = "Pull Cabbage",
        Description = "Click to Pull Cabbage",
        Callback = function()
            Window:Dialog({
                Title = "Title",
                Content = "This is a dialog",
                Buttons = {
                    {
                        Title = "Confirm",
                        Callback = function()
                                local player = game.Players.LocalPlayer
local character = player.Character or player.CharacterAdded:Wait()
local humanoidRootPart = character:WaitForChild("HumanoidRootPart")

for i = 1, 100 do
    local Cabbage = workspace.Farm.Cabbage:FindFirstChild("Cabbage" .. i)
    if Cabbage then
        Cabbage.CFrame = humanoidRootPart.CFrame
    end
end



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

 Tabs.General:AddButton({
        Title = "Pull Lobster",
        Description = "Click to Pull Lobster",
        Callback = function()
            Window:Dialog({
                Title = "Title",
                Content = "This is a dialog",
                Buttons = {
                    {
                        Title = "Confirm",
                        Callback = function()
                                local player = game.Players.LocalPlayer
local character = player.Character or player.CharacterAdded:Wait()
local humanoidRootPart = character:WaitForChild("HumanoidRootPart")

for i = 1, 100 do
    local Lobster = workspace.Farm.Lobster:FindFirstChild("Lobster" .. i)
    if Lobster then
        Lobster.CFrame = humanoidRootPart.CFrame
    end
end



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

 Tabs.General:AddButton({
        Title = "Pull Rice",
        Description = "Click to Pull Rice",
        Callback = function()
            Window:Dialog({
                Title = "Title",
                Content = "This is a dialog",
                Buttons = {
                    {
                        Title = "Confirm",
                        Callback = function()
                                local player = game.Players.LocalPlayer
local character = player.Character or player.CharacterAdded:Wait()
local humanoidRootPart = character:WaitForChild("HumanoidRootPart")

for i = 1, 100 do
    local Rice = workspace.Farm.Rice:FindFirstChild("Rice" .. i)
    if Rice then
        Rice.CFrame = humanoidRootPart.CFrame
    end
end



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

 Tabs.General:AddButton({
        Title = "Pull Oil",
        Description = "Click to Pull Oil",
        Callback = function()
            Window:Dialog({
                Title = "Title",
                Content = "This is a dialog",
                Buttons = {
                    {
                        Title = "Confirm",
                        Callback = function()
                                local player = game.Players.LocalPlayer
local character = player.Character or player.CharacterAdded:Wait()
local humanoidRootPart = character:WaitForChild("HumanoidRootPart")

for i = 1, 100 do
    local Oil = workspace.Farm.Oil:FindFirstChild("Oil" .. i)
    if Oil then
        Oil.CFrame = humanoidRootPart.CFrame
    end
end



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
 Tabs.General:AddButton({
        Title = "Pull Crab",
        Description = "Click to Pull Crab",
        Callback = function()
            Window:Dialog({
                Title = "Title",
                Content = "This is a dialog",
                Buttons = {
                    {
                        Title = "Confirm",
                        Callback = function()
                                local player = game.Players.LocalPlayer
local character = player.Character or player.CharacterAdded:Wait()
local humanoidRootPart = character:WaitForChild("HumanoidRootPart")

for i = 1, 100 do
    local Crab = workspace.Farm.Crab:FindFirstChild("Crab" .. i)
    if Crab then
        Crab.CFrame = humanoidRootPart.CFrame
    end
end



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
 Tabs.General:AddButton({
        Title = "Pull Pumpkin",
        Description = "Click to Pull Pumpkin",
        Callback = function()
            Window:Dialog({
                Title = "Title",
                Content = "This is a dialog",
                Buttons = {
                    {
                        Title = "Confirm",
                        Callback = function()
                                local player = game.Players.LocalPlayer
local character = player.Character or player.CharacterAdded:Wait()
local humanoidRootPart = character:WaitForChild("HumanoidRootPart")

for i = 1, 100 do
    local Pumpkin = workspace.Farm.Pumpkin:FindFirstChild("Pumpkin" .. i)
    if Pumpkin then
        Pumpkin.CFrame = humanoidRootPart.CFrame
    end
end



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

 Tabs.General:AddButton({
        Title = "Pull Strawberry",
        Description = "Click to Pull Strawberry",
        Callback = function()
            Window:Dialog({
                Title = "Title",
                Content = "This is a dialog",
                Buttons = {
                    {
                        Title = "Confirm",
                        Callback = function()
                                local player = game.Players.LocalPlayer
local character = player.Character or player.CharacterAdded:Wait()
local humanoidRootPart = character:WaitForChild("HumanoidRootPart")

for i = 1, 100 do
    local Strawberry = workspace.Farm.Strawberry:FindFirstChild("Strawberry" .. i)
    if Strawberry then
        Strawberry.CFrame = humanoidRootPart.CFrame
    end
end



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
 Tabs.General:AddButton({
        Title = "Pull Orange",
        Description = "Click to Pull Orange",
        Callback = function()
            Window:Dialog({
                Title = "Title",
                Content = "This is a dialog",
                Buttons = {
                    {
                        Title = "Confirm",
                        Callback = function()
                                local player = game.Players.LocalPlayer
local character = player.Character or player.CharacterAdded:Wait()
local humanoidRootPart = character:WaitForChild("HumanoidRootPart")

for i = 1, 100 do
    local Orange = workspace.Farm.Orange:FindFirstChild("Orange" .. i)
    if Orange then
        Orange.CFrame = humanoidRootPart.CFrame
    end
end



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
Tabs.General:AddButton({
        Title = "Pull Meat",
        Description = "Click to Pull Meat",
        Callback = function()
            Window:Dialog({
                Title = "Title",
                Content = "This is a dialog",
                Buttons = {
                    {
                        Title = "Confirm",
                        Callback = function()
                                local player = game.Players.LocalPlayer
local character = player.Character or player.CharacterAdded:Wait()
local humanoidRootPart = character:WaitForChild("HumanoidRootPart")

for i = 1, 100 do
    local Meat = workspace.Farm.Meat:FindFirstChild("Meat" .. i)
    if Meat then
        Meat.CFrame = humanoidRootPart.CFrame
    end
end



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
Tabs.General:AddButton({
        Title = "Pull Scrap",
        Description = "Click to Pull Scrap",
        Callback = function()
            Window:Dialog({
                Title = "Title",
                Content = "This is a dialog",
                Buttons = {
                    {
                        Title = "Confirm",
                        Callback = function()
                                local player = game.Players.LocalPlayer
local character = player.Character or player.CharacterAdded:Wait()
local humanoidRootPart = character:WaitForChild("HumanoidRootPart")

for i = 1, 100 do
    local Scrap = workspace.Farm.Scrap:FindFirstChild("Scrap" .. i)
    if Scrap then
        Scrap.CFrame = humanoidRootPart.CFrame
    end
end



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
 Tabs.General:AddButton({
        Title = "Pull Stone",
        Description = "Click to Pull Stone",
        Callback = function()
            Window:Dialog({
                Title = "Title",
                Content = "This is a dialog",
                Buttons = {
                    {
                        Title = "Confirm",
                        Callback = function()
                                local player = game.Players.LocalPlayer
local character = player.Character or player.CharacterAdded:Wait()
local humanoidRootPart = character:WaitForChild("HumanoidRootPart")

for i = 1, 100 do
    local Stone = workspace.Farm.Stone:FindFirstChild("Stone" .. i)
    if Stone then
        Stone.CFrame = humanoidRootPart.CFrame
    end
end



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

Tabs.General:AddButton({
        Title = "Pull Apple",
        Description = "Click to Pull Apple",
        Callback = function()
            Window:Dialog({
                Title = "Title",
                Content = "This is a dialog",
                Buttons = {
                    {
                        Title = "Confirm",
                        Callback = function()
                                local player = game.Players.LocalPlayer
local character = player.Character or player.CharacterAdded:Wait()
local humanoidRootPart = character:WaitForChild("HumanoidRootPart")

for i = 1, 100 do
    local Apple = workspace.Farm.Apple:FindFirstChild("Apple" .. i)
    if Apple then
        Apple.CFrame = humanoidRootPart.CFrame
    end
end



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


Tabs.General:AddButton({
        Title = "Pull Mushroom",
        Description = "Click to Pull Mushroom",
        Callback = function()
            Window:Dialog({
                Title = "Title",
                Content = "This is a dialog",
                Buttons = {
                    {
                        Title = "Confirm",
                        Callback = function()
                                local player = game.Players.LocalPlayer
local character = player.Character or player.CharacterAdded:Wait()
local humanoidRootPart = character:WaitForChild("HumanoidRootPart")

for i = 1, 100 do
    local Mushroom = workspace.Farm.Mushroom:FindFirstChild("Mushroom" .. i)
    if Mushroom then
        Mushroom.CFrame = humanoidRootPart.CFrame
    end
end



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



Tabs.General:AddButton({
        Title = "Pull Wood",
        Description = "Click to Pull Wood",
        Callback = function()
            Window:Dialog({
                Title = "Title",
                Content = "This is a dialog",
                Buttons = {
                    {
                        Title = "Confirm",
                        Callback = function()
                                local player = game.Players.LocalPlayer
local character = player.Character or player.CharacterAdded:Wait()
local humanoidRootPart = character:WaitForChild("HumanoidRootPart")

for i = 1, 100 do
    local Wood = workspace.Farm.Wood:FindFirstChild("Wood" .. i)
    if Wood then
        Wood.CFrame = humanoidRootPart.CFrame
    end
end



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
-- เพิ่ม Slider
local Slider = Tabs.playes:AddSlider("Slider", {
    Title = "Speed ",
    Description = "click to Increase speed",
    Default = 0.5,
    Min = 0,
    Max = 100,
    Rounding = 1,
    Callback = function(Value)
        -- กำหนดความเร็วของตัวละครตามค่าจากสไลเดอร์
        local humanoid = game.Players.LocalPlayer.Character:FindFirstChild("Humanoid")
        if humanoid then
            humanoid.WalkSpeed = Value * 16  -- เพิ่มความเร็วตามค่าจากสไลเดอร์
            print("Slider was changed:", Value)
        end
    end
})

Slider:OnChanged(function(Value)
    print("Slider changed:", Value)
end)


    Tabs.playes:AddButton({
        Title = "NoClip",
        Description = "click to NoClip",
        Callback = function()
            Window:Dialog({
                Title = "Title",
                Content = "This is a dialog",
                Buttons = {
                    {
                        Title = "Confirm",
                        Callback = function()
                            local player = game.Players.LocalPlayer
local character = player.Character or player.CharacterAdded:Wait()
local noclipEnabled = false -- ตัวแปรเปิด/ปิด NoClip

-- ฟังก์ชันเปิด NoClip
local function enableNoClip()
    noclipEnabled = true
    game:GetService("RunService").Stepped:Connect(function()
        if noclipEnabled and character then
            for _, part in pairs(character:GetDescendants()) do
                if part:IsA("BasePart") and part.CanCollide then
                    part.CanCollide = false
                end
            end
        end
    end)
end

-- ฟังก์ชันปิด NoClip
local function disableNoClip()
    noclipEnabled = false
    if character then
        for _, part in pairs(character:GetDescendants()) do
            if part:IsA("BasePart") then
                part.CanCollide = true
            end
        end
    end
end

-- การสลับสถานะด้วยการกดปุ่ม (ตัวอย่าง: ปุ่ม "N")
local UIS = game:GetService("UserInputService")
UIS.InputBegan:Connect(function(input, isProcessed)
    if not isProcessed and input.KeyCode == Enum.KeyCode.N then
        if noclipEnabled then
            disableNoClip()
        else
            enableNoClip()
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



    Tabs.playes:AddButton({
        Title = "Respawn playes",
        Description = "click to Respawn playes",
        Callback = function()
            Window:Dialog({
                Title = "Title",
                Content = "This is a dialog",
                Buttons = {
                    {
                        Title = "Confirm",
                        Callback = function()
                             local args = {
 [1] = "Respawn",
 [2] = game:GetService("Players").LocalPlayer
}

game:GetService("ReplicatedStorage"):WaitForChild("ReviveSystem"):WaitForChild("Event"):FireServer(unpack(args))
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

Tabs.lsland:AddParagraph({
        Title = "---------------------------------------- lsland Farm ↓ ---------------------------",
        Content = ""
    })

 local Dropdown = Tabs.lsland:AddDropdown("Dropdown", {
    Title = "Dropdown",
    Values = {"Wood", "Watermelon", "Chest_Box", "Strawberry", "Rice", "Stone", "Banana", "Cabbage", "Scrap", "Oil", "Cactus", "Oil", "Oil", "Oil", "Cabbage"  },
    Multi = false,
    Default = ""
})

Dropdown:SetValue("four")

Dropdown:OnChanged(function(Value)
    print("Dropdown changed:", Value)
    local player = game.Players.LocalPlayer
    if player and player.Character and player.Character:FindFirstChild("HumanoidRootPart") then
        if Value == "Wood" then
            player.Character.HumanoidRootPart.CFrame = CFrame.new(2616, 59, -2616)
        elseif Value == "Watermelon" then
            player.Character.HumanoidRootPart.CFrame = CFrame.new(3426, 21, -366)
        elseif Value == "Chest_Box" then
            player.Character.HumanoidRootPart.CFrame = CFrame.new(3778, 2, -531)
       elseif Value == "Strawberry" then
            player.Character.HumanoidRootPart.CFrame = CFrame.new(2802, 98, -619)
       elseif Value == "Rice" then
            player.Character.HumanoidRootPart.CFrame = CFrame.new(2296, 15, -260)
       elseif Value == "Stone" then
            player.Character.HumanoidRootPart.CFrame = CFrame.new(1486, -5, -928)            
       elseif Value == "Banana" then
            player.Character.HumanoidRootPart.CFrame = CFrame.new(-3133, 18, -799)
        elseif Value == "Cabbage" then
            player.Character.HumanoidRootPart.CFrame = CFrame.new(-508, 22, -2536)  
        elseif Value == "Scrap" then
            player.Character.HumanoidRootPart.CFrame = CFrame.new(-512, 72, -3997) 
        elseif Value == "Oil" then
            player.Character.HumanoidRootPart.CFrame = CFrame.new(-260, 120, -3839)
         elseif Value == "Cactus" then
            player.Character.HumanoidRootPart.CFrame = CFrame.new(-819, 14, -4680)                
        end
    end
end)
