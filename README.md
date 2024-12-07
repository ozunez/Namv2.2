local player = game.Players.LocalPlayer
local gui = Instance.new("ScreenGui", player:WaitForChild("PlayerGui"))
local frame = Instance.new("Frame", gui)
frame.Size, frame.Position = UDim2.new(0.3, 0, 0.2, 0), UDim2.new(0.35, 0, 0.4, 0)
frame.BackgroundColor3, frame.BorderSizePixel = Color3.fromRGB(42, 42, 42), 0
Instance.new("UICorner", frame).CornerRadius = UDim.new(0, 15)

local label = Instance.new("TextLabel", frame)
label.Text, label.Size, label.Position = "Enter Key", UDim2.new(1, 0, 0.2, 0), UDim2.new(0, 0, 0, 0)
label.TextColor3, label.BackgroundTransparency, label.TextScaled = Color3.fromRGB(255, 255, 255), 1, true

local textBox = Instance.new("TextBox", frame)
textBox.Size, textBox.Position = UDim2.new(0.9, 0, 0.3, 0), UDim2.new(0.05, 0, 0.3, 0)
textBox.PlaceholderText, textBox.TextColor3 = "Enter Key Here", Color3.fromRGB(255, 255, 255)
textBox.BackgroundColor3, textBox.BorderSizePixel = Color3.fromRGB(60, 60, 60), 0
Instance.new("UICorner", textBox).CornerRadius = UDim.new(0, 10)

local submit = Instance.new("TextButton", frame)
submit.Size, submit.Position = UDim2.new(0.9, 0, 0.3, 0), UDim2.new(0.05, 0, 0.65, 0)
submit.Text, submit.TextColor3, submit.BackgroundColor3 = "Submit", Color3.fromRGB(255, 255, 255), Color3.fromRGB(34, 139, 34)
Instance.new("UICorner", submit).CornerRadius = UDim.new(0, 10)

-- ตารางเก็บ ID และคีย์
local keys = {
    [5370483427] = "dev", -- ID: คีย์
    [7144504097] = "Dev",
    [1234567890] = "exampleKey", -- เพิ่ม ID และคีย์ใหม่ได้ที่นี่
    [9876543210] = "secretCode"
}

local function submitKey()
    local input, id = textBox.Text, player.UserId
    local correctKey = keys[id] -- ดึงคีย์จาก ID ในตาราง
    if correctKey and input == correctKey then
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
    Dupe = Window:AddTab({ Title = "🥽Duped", Icon = "Duped" }),
    Weapon = Window:AddTab({ Title = "🔫Weapon", Icon = "Weapon" })
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

local Toggle = Tabs.playes:AddToggle("MyToggle", {Title = "Auto Eat", Default = false })

local running = false -- ตัวแปรเพื่อตรวจสอบสถานะการทำงานของลูป

Toggle:OnChanged(function(state)
    local player = game:GetService("Players").LocalPlayer

    -- ตรวจสอบสถานะของ Toggle
    if state then
        if not running then
            running = true  -- ตั้งค่าตัวแปร running เป็น true เพื่อเริ่มลูป
            spawn(function()  -- ใช้ spawn เพื่อให้สามารถหยุดการทำงานได้ทันที
                while true do
                    -- ตรวจสอบ Hunger
                    local hunger = player.Status.Hunger.Value
                    if hunger < 50 then
                        local args = {
                            [1] = "Use",
                            [2] = "Bread"
                        }
                        game:GetService("ReplicatedStorage"):WaitForChild("Remote"):WaitForChild("Inventory"):FireServer(unpack(args))
                        wait(0.2)
                        local args = {
                            [1] = "Store",
                            [2] = "Bread",
                            [3] = 1
                        }
                        game:GetService("ReplicatedStorage"):WaitForChild("Remote"):WaitForChild("Vault"):FireServer(unpack(args))
                        wait(30)
                        local args = {
                            [1] = "Get",
                            [2] = "Bread",
                            [3] = 1
                        }
                        game:GetService("ReplicatedStorage"):WaitForChild("Remote"):WaitForChild("Vault"):FireServer(unpack(args))
                    end

                    -- ตรวจสอบ Shield (สมมติว่าเก็บในค่า Hunger)
                    local Shield = player.Status.Hunger.Value
                    if Shield > 50 then
                        local args = {
                            [1] = "Use",
                            [2] = "Tea"
                        }
                        game:GetService("ReplicatedStorage"):WaitForChild("Remote"):WaitForChild("Inventory"):FireServer(unpack(args))
                        wait(0.2)
                        local args = {
                            [1] = "Store",
                            [2] = "Tea",
                            [3] = 1
                        }
                        game:GetService("ReplicatedStorage"):WaitForChild("Remote"):WaitForChild("Vault"):FireServer(unpack(args))
                        wait(30)
                        local args = {
                            [1] = "Get",
                            [2] = "Tea",
                            [3] = 1
                        }
                        game:GetService("ReplicatedStorage"):WaitForChild("Remote"):WaitForChild("Vault"):FireServer(unpack(args))
                    end

                    -- ตรวจสอบ Thirsty
                    local Thirsty = player.Status.Hunger.Value
                    if Thirsty < 50 then
                        local args = {
                            [1] = "Use",
                            [2] = "Water"
                        }
                        game:GetService("ReplicatedStorage"):WaitForChild("Remote"):WaitForChild("Inventory"):FireServer(unpack(args))
                        wait(0.2)
                        local args = {
                            [1] = "Store",
                            [2] = "Water",
                            [3] = 1
                        }
                        game:GetService("ReplicatedStorage"):WaitForChild("Remote"):WaitForChild("Vault"):FireServer(unpack(args))
                        wait(30)
                        local args = {
                            [1] = "Get",
                            [2] = "Water",
                            [3] = 1
                        }
                        game:GetService("ReplicatedStorage"):WaitForChild("Remote"):WaitForChild("Vault"):FireServer(unpack(args))
                    end

                    -- รอ 60 วินาที ก่อนทำงานต่อ
                    wait(60)

                    -- ตรวจสอบสถานะของ Toggle ทุกครั้งก่อนทำงานใหม่
                    if not state then
                        running = false  -- หยุดการทำงานเมื่อ Toggle ปิด
                        break  -- ออกจากลูปถ้าปิด Toggle
                    end
                end
            end)
        end
    else
        -- ถ้า Toggle ปิด ให้หยุดการทำงานของลูป
        running = false
    end
end)


Tabs.lsland:AddParagraph({
        Title = "---------------------------------------- lsland Farm ↓ ---------------------------",
        Content = ""
    })

 local Dropdown = Tabs.lsland:AddDropdown("Dropdown", {
    Title = "Dropdown",
    Values = {"Wood", "Watermelon", "Chest_Box", "Strawberry", "Rice", "Stone", "Banana", "Cabbage", "Scrap", "Oil", "Cactus", "Crab", "Lobster", "Meat", "Orange", "Apple", "Pumpkin"  },
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
         elseif Value == "Crab" then
            player.Character.HumanoidRootPart.CFrame = CFrame.new(-791, 12, -5036) 
         elseif Value == "Lobster" then
            player.Character.HumanoidRootPart.CFrame = CFrame.new(-1251, 19, -5052)  
         elseif Value == "Meat" then
            player.Character.HumanoidRootPart.CFrame = CFrame.new(338, 199, -4303)      
         elseif Value == "Orange" then
            player.Character.HumanoidRootPart.CFrame = CFrame.new(569, 193, -5506)    
         elseif Value == "Apple" then
            player.Character.HumanoidRootPart.CFrame = CFrame.new(2308, 68, -6144)       
        elseif Value == "Pumpkin" then
            player.Character.HumanoidRootPart.CFrame = CFrame.new(2054, 314, -5574)                
        end
    end
end)
local Dropdown = Tabs.lsland:AddDropdown("Dropdown", {
    Title = "Vault And Crafting Table",
    Values = {"Vault Rebel", "Vault Spawn", "Vault Hospital", "Crafting Table", "Bed" },
    Multi = false,
    Default = ""
})

Dropdown:SetValue("four")

Dropdown:OnChanged(function(Value)
    print("Dropdown changed:", Value)
    local player = game.Players.LocalPlayer
    if player and player.Character and player.Character:FindFirstChild("HumanoidRootPart") then
        if Value == "Vault Rebel" then
            player.Character.HumanoidRootPart.CFrame = CFrame.new(-1108.5020751953125, 85.4330062866211, -663.6085205078125)
         elseif Value == "Vault Spawn" then
            player.Character.HumanoidRootPart.CFrame = CFrame.new(584.4301147460938, 21.486005783081055, 294.83197021484375)
         elseif Value == "Vault Hospital" then
            player.Character.HumanoidRootPart.CFrame = CFrame.new(3517.265380859375, 21.27487564086914, -2822.075927734375)
         elseif Value == "Crafting Table" then
            player.Character.HumanoidRootPart.CFrame = CFrame.new(-1140.59423828125, 85.44157409667969, -663.7395629882812)
         elseif Value == "Bed" then
            player.Character.HumanoidRootPart.CFrame = CFrame.new(3538.2626953125, 21.274879455566406, -2927.361572265625)               
        end
    end
end)
Tabs.Dupe:AddParagraph({
        Title = "---------------------------------------- Dupe Item ↓ --------------------------------",
        Content = ""
    })


    Tabs.Dupe:AddButton({
        Title = "Dupe",
        Description = "Dupe Item",
        Callback = function()
            Window:Dialog({
                Title = "Warning",
                Content = "This Will Lag!",
                Buttons = {
                    {
                        Title = "Confirm",
                        Callback = function()
                            local player = game.Players.LocalPlayer
local character = player.Character or player.CharacterAdded:Wait()

if character:FindFirstChild("Humanoid") then
    character.Humanoid.Health = 0
end

Wait(2)

for i = 1, 99999 do
    local args = {
 [1] = "Respawn",
 [2] = game:GetService("Players").LocalPlayer
}

game:GetService("ReplicatedStorage"):WaitForChild("ReviveSystem"):WaitForChild("Event"):FireServer(unpack(args))
end
for i = 1, 99999 do
    local args = {
 [1] = "Respawn",
 [2] = game:GetService("Players").LocalPlayer
}

game:GetService("ReplicatedStorage"):WaitForChild("ReviveSystem"):WaitForChild("Event"):FireServer(unpack(args))
end
for i = 1, 99999 do
    local args = {
 [1] = "Respawn",
 [2] = game:GetService("Players").LocalPlayer
}

game:GetService("ReplicatedStorage"):WaitForChild("ReviveSystem"):WaitForChild("Event"):FireServer(unpack(args))
end
for i = 1, 99999 do
    local args = {
 [1] = "Respawn",
 [2] = game:GetService("Players").LocalPlayer
}

game:GetService("ReplicatedStorage"):WaitForChild("ReviveSystem"):WaitForChild("Event"):FireServer(unpack(args))
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

local Toggle = Tabs.Dupe:AddToggle("MyToggle", {Title = "Dupe Money", Default = false })

local running = false -- ใช้ตัวแปรเพื่อติดตามสถานะการทำงาน

Toggle:OnChanged(function(state)
    running = state -- กำหนดสถานะการทำงานตาม Toggle
    if running then
        -- โค้ดจะทำงานเมื่อ Toggle ถูกเปิด
        local player = game.Players.LocalPlayer
        local character = player.Character or player.CharacterAdded:Wait()

        if character and character:FindFirstChild("HumanoidRootPart") then
            character.HumanoidRootPart.CFrame = CFrame.new(574, 21, 326)
        end
        wait(1)

        for i = 1, 999 do
            if not running then break end -- หยุดลูปหาก Toggle ถูกปิด
            local args = {
                [1] = "Tea",
                [2] = -1
            }

            game:GetService("ReplicatedStorage"):WaitForChild("Remote"):WaitForChild("Shop"):FireServer(unpack(args))
            wait(0.2) -- รอ 0.5 วินาทีก่อนที่จะส่งคำสั่งถัดไป
        end
    end
end)


Tabs.Dupe:AddParagraph({
        Title = "---------------------------------------- Dupe food ↓ --------------------------------",
        Content = ""
    })

    Tabs.Dupe:AddButton({
        Title = "Dupe Tea",
        Description = "Dupe to Tea",
        Callback = function()
            Window:Dialog({
                Title = "Title",
                Content = "This is a dialog",
                Buttons = {
                    {
                        Title = "Confirm",
                        Callback = function()
                            local args = {
            [1] = "Use",
            [2] = "Tea"
        }
        game:GetService("ReplicatedStorage"):WaitForChild("Remote"):WaitForChild("Inventory"):FireServer(unpack(args))
wait(0.2)
local args = {
    [1] = "Store",
    [2] = "Tea",
    [3] = 1
}

game:GetService("ReplicatedStorage"):WaitForChild("Remote"):WaitForChild("Vault"):FireServer(unpack(args))
wait(30)
local args = {
    [1] = "Get",
    [2] = "Tea",
    [3] = 1
}

game:GetService("ReplicatedStorage"):WaitForChild("Remote"):WaitForChild("Vault"):FireServer(unpack(args))
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

 Tabs.Dupe:AddButton({
        Title = "Dupe Bread",
        Description = "Dupe to Bread",
        Callback = function()
            Window:Dialog({
                Title = "Title",
                Content = "This is a dialog",
                Buttons = {
                    {
                        Title = "Confirm",
                        Callback = function()
                            local args = {
            [1] = "Use",
            [2] = "Bread"
        }
        game:GetService("ReplicatedStorage"):WaitForChild("Remote"):WaitForChild("Inventory"):FireServer(unpack(args))
wait(0.2)
local args = {
    [1] = "Store",
    [2] = "Bread",
    [3] = 1
}

game:GetService("ReplicatedStorage"):WaitForChild("Remote"):WaitForChild("Vault"):FireServer(unpack(args))
wait(30)
local args = {
    [1] = "Get",
    [2] = "Bread",
    [3] = 1
}

game:GetService("ReplicatedStorage"):WaitForChild("Remote"):WaitForChild("Vault"):FireServer(unpack(args))
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

Tabs.Dupe:AddButton({
        Title = "Dupe Water",
        Description = "Dupe to Water",
        Callback = function()
            Window:Dialog({
                Title = "Title",
                Content = "This is a dialog",
                Buttons = {
                    {
                        Title = "Confirm",
                        Callback = function()
                            local args = {
            [1] = "Use",
            [2] = "Water"
        }
        game:GetService("ReplicatedStorage"):WaitForChild("Remote"):WaitForChild("Inventory"):FireServer(unpack(args))
wait(0.2)
local args = {
    [1] = "Store",
    [2] = "Water",
    [3] = 1
}

game:GetService("ReplicatedStorage"):WaitForChild("Remote"):WaitForChild("Vault"):FireServer(unpack(args))
wait(30)
local args = {
    [1] = "Get",
    [2] = "Water",
    [3] = 1
}

game:GetService("ReplicatedStorage"):WaitForChild("Remote"):WaitForChild("Vault"):FireServer(unpack(args))
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

Tabs.Dupe:AddParagraph({
        Title = "---------------------------------------- Dupe Hp ↓ --------------------------------",
        Content = ""
    })

    Tabs.Dupe:AddButton({
        Title = "Dupe Armor",
        Description = "Dupe to Armor",
        Callback = function()
            Window:Dialog({
                Title = "Title",
                Content = "This is a dialog",
                Buttons = {
                    {
                        Title = "Confirm",
                        Callback = function()
                           
    local args = {
        [1] = "Use",
        [2] = "Armor"
    }
    game:GetService("ReplicatedStorage"):WaitForChild("Remote"):WaitForChild("Inventory"):FireServer(unpack(args))
    wait(0.2)
    
    local args = {
        [1] = "Store",
        [2] = "Armor",
        [3] = 1
    }
    game:GetService("ReplicatedStorage"):WaitForChild("Remote"):WaitForChild("Vault"):FireServer(unpack(args))
    wait(3)
    
    local args = {
        [1] = "Get",
        [2] = "Armor",
        [3] = 1
    }
    game:GetService("ReplicatedStorage"):WaitForChild("Remote"):WaitForChild("Vault"):FireServer(unpack(args))



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

Tabs.Dupe:AddButton({
        Title = "Dupe Bandage",
        Description = "Dupe to Bandage",
        Callback = function()
            Window:Dialog({
                Title = "Title",
                Content = "This is a dialog",
                Buttons = {
                    {
                        Title = "Confirm",
                        Callback = function()
                            local args = {
            [1] = "Use",
            [2] = "Bandage"
        }
        game:GetService("ReplicatedStorage"):WaitForChild("Remote"):WaitForChild("Inventory"):FireServer(unpack(args))
wait(0.2)
local args = {
    [1] = "Store",
    [2] = "Bandage",
    [3] = 1
}

game:GetService("ReplicatedStorage"):WaitForChild("Remote"):WaitForChild("Vault"):FireServer(unpack(args))
wait(1.7)
local args = {
    [1] = "Get",
    [2] = "Bandage",
    [3] = 1
}

game:GetService("ReplicatedStorage"):WaitForChild("Remote"):WaitForChild("Vault"):FireServer(unpack(args))
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

Tabs.Dupe:AddParagraph({
        Title = "---------------------------------------- Dupe Hp ↓ --------------------------------",
        Content = "    ------------------------------ Key Binds (X,Z) --------------------------------"
    })

Tabs.Dupe:AddButton({
        Title = "Dupe Armor",
        Description = "Dupe to Armor",
        Callback = function()
            Window:Dialog({
                Title = "Warning",
                Content = "This Bind X",
                Buttons = {
                    {
                        Title = "Confirm",
                        Callback = function()
                           local UserInputService = game:GetService("UserInputService")

-- Function to execute your sequence
local function executeSequence()
    local args = {
        [1] = "Use",
        [2] = "Armor"
    }
    game:GetService("ReplicatedStorage"):WaitForChild("Remote"):WaitForChild("Inventory"):FireServer(unpack(args))
    wait(0.2)
    
    local args = {
        [1] = "Store",
        [2] = "Armor",
        [3] = 1
    }
    game:GetService("ReplicatedStorage"):WaitForChild("Remote"):WaitForChild("Vault"):FireServer(unpack(args))
    wait(3)
    
    local args = {
        [1] = "Get",
        [2] = "Armor",
        [3] = 1
    }
    game:GetService("ReplicatedStorage"):WaitForChild("Remote"):WaitForChild("Vault"):FireServer(unpack(args))
end

-- Bind the sequence to the "X" key
UserInputService.InputBegan:Connect(function(input, isProcessed)
    if isProcessed then return end -- Ignore if the input is already processed
    if input.KeyCode == Enum.KeyCode.X then
        executeSequence()
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
Tabs.Dupe:AddButton({
        Title = "Dupe Bandage",
        Description = "Dupe to Bandage",
        Callback = function()
            Window:Dialog({
                Title = "Warning",
                Content = "This Bind Z",
                Buttons = {
                    {
                        Title = "Confirm",
                        Callback = function()
local UserInputService = game:GetService("UserInputService")

-- Function to execute the Bandage sequence
local function executeBandageSequence()
    local args = {
        [1] = "Use",
        [2] = "Bandage"
    }
    game:GetService("ReplicatedStorage"):WaitForChild("Remote"):WaitForChild("Inventory"):FireServer(unpack(args))
    wait(0.2)
    
    local args = {
        [1] = "Store",
        [2] = "Bandage",
        [3] = 1
    }
    game:GetService("ReplicatedStorage"):WaitForChild("Remote"):WaitForChild("Vault"):FireServer(unpack(args))
    wait(1.7)
    
    local args = {
        [1] = "Get",
        [2] = "Bandage",
        [3] = 1
    }
    game:GetService("ReplicatedStorage"):WaitForChild("Remote"):WaitForChild("Vault"):FireServer(unpack(args))
end

-- Bind the sequence to the "Z" key
UserInputService.InputBegan:Connect(function(input, isProcessed)
    if isProcessed then return end -- Ignore if the input is already processed
    if input.KeyCode == Enum.KeyCode.Z then
        executeBandageSequence()
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

Tabs.Dupe:AddParagraph({
        Title = "------------------------------- Dupe Crafting item ↓ ----------------------",
        Content = ""
    })
local Input = Tabs.Dupe:AddInput("Input", {
    Title = "SteelBar",
    Default = "",
    Placeholder = "",
    Numeric = true, -- กำหนดให้ใส่ได้เฉพาะตัวเลข
    Finished = true, -- Callback จะถูกเรียกเมื่อกด Enter
    Callback = function(Value)
        local m = tonumber(Value) -- แปลงค่าที่ใส่เป็นตัวเลข
        if m then -- ตรวจสอบว่าค่าเป็นตัวเลข
            print("เปลี่ยนค่า m เป็น:", m)
            local args = {
                [1] = "Material",
                [2] = "SteelBar",
                [3] = m
            }
            game:GetService("ReplicatedStorage"):WaitForChild("Remote"):WaitForChild("Craft"):FireServer(unpack(args))
        else
            print("โปรดใส่ค่าที่เป็นตัวเลข!")
        end
    end
})

local Input = Tabs.Dupe:AddInput("Input", {
    Title = "EXP Coin",
    Default = "",
    Placeholder = "",
    Numeric = true, -- กำหนดให้ใส่ได้เฉพาะตัวเลข
    Finished = true, -- Callback จะถูกเรียกเมื่อกด Enter
    Callback = function(Value)
        local m = tonumber(Value) -- แปลงค่าที่ใส่เป็นตัวเลข
        if m then -- ตรวจสอบว่าค่าเป็นตัวเลข
            print("เปลี่ยนค่า m เป็น:", m)
            local args = {
                [1] = "Material",
                [2] = "EXP Coin",
                [3] = m
            }
            game:GetService("ReplicatedStorage"):WaitForChild("Remote"):WaitForChild("Craft"):FireServer(unpack(args))
        else
            print("โปรดใส่ค่าที่เป็นตัวเลข!")
        end
    end
})

local Input = Tabs.Dupe:AddInput("Input", {
    Title = "Bullet",
    Default = "",
    Placeholder = "",
    Numeric = true, -- กำหนดให้ใส่ได้เฉพาะตัวเลข
    Finished = true, -- Callback จะถูกเรียกเมื่อกด Enter
    Callback = function(Value)
        local m = tonumber(Value) -- แปลงค่าที่ใส่เป็นตัวเลข
        if m then -- ตรวจสอบว่าค่าเป็นตัวเลข
            print("เปลี่ยนค่า m เป็น:", m)
            local args = {
                [1] = "Material",
                [2] = "Bullet",
                [3] = m
            }
            game:GetService("ReplicatedStorage"):WaitForChild("Remote"):WaitForChild("Craft"):FireServer(unpack(args))
        else
            print("โปรดใส่ค่าที่เป็นตัวเลข!")
        end
    end
})
local Input = Tabs.Dupe:AddInput("Input", {
    Title = "Xmas Gacha",
    Default = "",
    Placeholder = "",
    Numeric = true, -- กำหนดให้ใส่ได้เฉพาะตัวเลข
    Finished = true, -- Callback จะถูกเรียกเมื่อกด Enter
    Callback = function(Value)
        local m = tonumber(Value) -- แปลงค่าที่ใส่เป็นตัวเลข
        if m then -- ตรวจสอบว่าค่าเป็นตัวเลข
            print("เปลี่ยนค่า m เป็น:", m)
            local args = {
                [1] = "Material",
                [2] = "Ch_Gacha",
                [3] = m
            }
            game:GetService("ReplicatedStorage"):WaitForChild("Remote"):WaitForChild("Craft"):FireServer(unpack(args))
        else
            print("โปรดใส่ค่าที่เป็นตัวเลข!")
        end
    end
})
local Input = Tabs.Dupe:AddInput("Input", {
    Title = "Star Card Upgrade",
    Default = "",
    Placeholder = "",
    Numeric = true, -- กำหนดให้ใส่ได้เฉพาะตัวเลข
    Finished = true, -- Callback จะถูกเรียกเมื่อกด Enter
    Callback = function(Value)
        local m = tonumber(Value) -- แปลงค่าที่ใส่เป็นตัวเลข
        if m then -- ตรวจสอบว่าค่าเป็นตัวเลข
            print("เปลี่ยนค่า m เป็น:", m)
            local args = {
                [1] = "Material",
                [2] = "Star_Card_Up",
                [3] = m
            }
            game:GetService("ReplicatedStorage"):WaitForChild("Remote"):WaitForChild("Craft"):FireServer(unpack(args))
        else
            print("โปรดใส่ค่าที่เป็นตัวเลข!")
        end
    end
})
local Input = Tabs.Dupe:AddInput("Input", {
    Title = "Star Card",
    Default = "",
    Placeholder = "",
    Numeric = true, -- กำหนดให้ใส่ได้เฉพาะตัวเลข
    Finished = true, -- Callback จะถูกเรียกเมื่อกด Enter
    Callback = function(Value)
        local m = tonumber(Value) -- แปลงค่าที่ใส่เป็นตัวเลข
        if m then -- ตรวจสอบว่าค่าเป็นตัวเลข
            print("เปลี่ยนค่า m เป็น:", m)
            local args = {
                [1] = "Material",
                [2] = "Star_Card",
                [3] = m
            }
            game:GetService("ReplicatedStorage"):WaitForChild("Remote"):WaitForChild("Craft"):FireServer(unpack(args))
        else
            print("โปรดใส่ค่าที่เป็นตัวเลข!")
        end
    end
})
local Input = Tabs.Dupe:AddInput("Input", {
    Title = "Gift Box",
    Default = "",
    Placeholder = "",
    Numeric = true, -- กำหนดให้ใส่ได้เฉพาะตัวเลข
    Finished = true, -- Callback จะถูกเรียกเมื่อกด Enter
    Callback = function(Value)
        local m = tonumber(Value) -- แปลงค่าที่ใส่เป็นตัวเลข
        if m then -- ตรวจสอบว่าค่าเป็นตัวเลข
            print("เปลี่ยนค่า m เป็น:", m)
            local args = {
                [1] = "Material",
                [2] = "Gift_Box",
                [3] = m
            }
            game:GetService("ReplicatedStorage"):WaitForChild("Remote"):WaitForChild("Craft"):FireServer(unpack(args))
        else
            print("โปรดใส่ค่าที่เป็นตัวเลข!")
        end
    end
})
local Input = Tabs.Dupe:AddInput("Input", {
    Title = "Mineral Purple",
    Default = "",
    Placeholder = "",
    Numeric = true, -- กำหนดให้ใส่ได้เฉพาะตัวเลข
    Finished = true, -- Callback จะถูกเรียกเมื่อกด Enter
    Callback = function(Value)
        local m = tonumber(Value) -- แปลงค่าที่ใส่เป็นตัวเลข
        if m then -- ตรวจสอบว่าค่าเป็นตัวเลข
            print("เปลี่ยนค่า m เป็น:", m)
            local args = {
                [1] = "Material",
                [2] = "Mineral_Purple",
                [3] = m
            }
            game:GetService("ReplicatedStorage"):WaitForChild("Remote"):WaitForChild("Craft"):FireServer(unpack(args))
        else
            print("โปรดใส่ค่าที่เป็นตัวเลข!")
        end
    end
})

Tabs.Weapon:AddParagraph({
        Title = "---------------------------------------- Emo ↓ ----------------------------------",
        Content = ""
    })

local Toggle = Tabs.Weapon:AddToggle("MyToggle", {Title = "Broken_Bottle", Default = false })



local UserInputService = game:GetService("UserInputService")
local Players = game:GetService("Players")
local player = Players.LocalPlayer

-- เก็บข้อมูลเพื่อจัดการการเชื่อมต่อ Event
local inputEvent
local deathEvent

-- ฟังก์ชันสำหรับโหลด Animation
local function loadAnimation(humanoid)
    local animationId = "rbxassetid://116546793402774"
    local animation = Instance.new("Animation")
    animation.AnimationId = animationId
    local animator = humanoid:FindFirstChild("Animator") or humanoid:WaitForChild("Animator")
    return animator:LoadAnimation(animation)
end

-- ฟังก์ชันหลักที่ทำงานเมื่อ Toggle เปิด
local function setupCharacter(character)
    local humanoid = character:WaitForChild("Humanoid")
    local animationTrack = loadAnimation(humanoid)

    -- เชื่อมต่อเมื่อกดปุ่ม Q
    inputEvent = UserInputService.InputBegan:Connect(function(input, gameProcessed)
        if Toggle.Value and not gameProcessed and input.KeyCode == Enum.KeyCode.Q then
            -- รันท่าทาง
            animationTrack:Play()

            -- รันคำสั่ง for-loop
            for i = 1, 6 do
                local weaponName = "Broken_BottleUpgrade" .. i
                local weapon = character:FindFirstChild(weaponName)

                if weapon then
                    local args = {
                        [1] = weapon.Handle
                    }
                    weapon.Combo.Emo:FireServer(unpack(args))
                else
                    warn(weaponName .. " not found in character!")
                end
            end
        end
    end)

    -- รีเซ็ตเมื่อผู้เล่นตาย
    deathEvent = humanoid.Died:Connect(function()
        if Toggle.Value then
            print("Player has died. Resetting...")
            player.CharacterAdded:Wait()
            setupCharacter(player.Character)
        end
    end)
end

-- เช็คว่า Toggle เปิดหรือปิด
Toggle:OnChanged(function(isEnabled)
    if isEnabled then
        -- เริ่มต้นการทำงานเมื่อ Toggle เปิด
        if player.Character then
            setupCharacter(player.Character)
        end
        player.CharacterAdded:Connect(setupCharacter)
    else
        -- ยกเลิกการเชื่อมต่อ Event เมื่อ Toggle ปิด
        if inputEvent then inputEvent:Disconnect() end
        if deathEvent then deathEvent:Disconnect() end
    end
end)

local Toggle = Tabs.Weapon:AddToggle("MyToggle", {Title = "M9", Default = false })



local UserInputService = game:GetService("UserInputService")
local Players = game:GetService("Players")
local player = Players.LocalPlayer

-- เก็บข้อมูลเพื่อจัดการการเชื่อมต่อ Event
local inputEvent
local deathEvent

-- ฟังก์ชันสำหรับโหลด Animation
local function loadAnimation(humanoid)
    local animationId = "rbxassetid://116546793402774"
    local animation = Instance.new("Animation")
    animation.AnimationId = animationId
    local animator = humanoid:FindFirstChild("Animator") or humanoid:WaitForChild("Animator")
    return animator:LoadAnimation(animation)
end

-- ฟังก์ชันหลักที่ทำงานเมื่อ Toggle เปิด
local function setupCharacter(character)
    local humanoid = character:WaitForChild("Humanoid")
    local animationTrack = loadAnimation(humanoid)

    -- เชื่อมต่อเมื่อกดปุ่ม Q
    inputEvent = UserInputService.InputBegan:Connect(function(input, gameProcessed)
        if Toggle.Value and not gameProcessed and input.KeyCode == Enum.KeyCode.Q then
            -- รันท่าทาง
            animationTrack:Play()

            -- รันคำสั่ง for-loop
            for i = 1, 6 do
                local weaponName = "M9Upgrade" .. i
                local weapon = character:FindFirstChild(weaponName)

                if weapon then
                    local args = {
                        [1] = weapon.Handle
                    }
                    weapon.Combo.Emo:FireServer(unpack(args))
                else
                    warn(weaponName .. " not found in character!")
                end
            end
        end
    end)

    -- รีเซ็ตเมื่อผู้เล่นตาย
    deathEvent = humanoid.Died:Connect(function()
        if Toggle.Value then
            print("Player has died. Resetting...")
            player.CharacterAdded:Wait()
            setupCharacter(player.Character)
        end
    end)
end

-- เช็คว่า Toggle เปิดหรือปิด
Toggle:OnChanged(function(isEnabled)
    if isEnabled then
        -- เริ่มต้นการทำงานเมื่อ Toggle เปิด
        if player.Character then
            setupCharacter(player.Character)
        end
        player.CharacterAdded:Connect(setupCharacter)
    else
        -- ยกเลิกการเชื่อมต่อ Event เมื่อ Toggle ปิด
        if inputEvent then inputEvent:Disconnect() end
        if deathEvent then deathEvent:Disconnect() end
    end
end)

Tabs.Weapon:AddParagraph({
        Title = "---------------------------------------- Kie ↓ ----------------------------------",
        Content = ""
    })


local Toggle = Tabs.Weapon:AddToggle("MyToggle", {Title = "Bat_Red", Default = false })



local UserInputService = game:GetService("UserInputService")
local Players = game:GetService("Players")
local player = Players.LocalPlayer

-- เก็บข้อมูลเพื่อจัดการการเชื่อมต่อ Event
local inputEvent
local deathEvent

-- ฟังก์ชันสำหรับโหลด Animation
local function loadAnimation(humanoid)
    local animationId = "rbxassetid://122516524039190"
    local animation = Instance.new("Animation")
    animation.AnimationId = animationId
    local animator = humanoid:FindFirstChild("Animator") or humanoid:WaitForChild("Animator")
    return animator:LoadAnimation(animation)
end

-- ฟังก์ชันหลักที่ทำงานเมื่อ Toggle เปิด
local function setupCharacter(character)
    local humanoid = character:WaitForChild("Humanoid")
    local animationTrack = loadAnimation(humanoid)

    -- เชื่อมต่อเมื่อกดปุ่ม Q
    inputEvent = UserInputService.InputBegan:Connect(function(input, gameProcessed)
        if Toggle.Value and not gameProcessed and input.KeyCode == Enum.KeyCode.Q then
            -- รันท่าทาง
            animationTrack:Play()

            -- รันคำสั่ง for-loop
            for i = 1, 6 do
                local weaponName = "Bat_RedUpgrade" .. i
                local weapon = character:FindFirstChild(weaponName)

                if weapon then
                    local args = {
                        [1] = weapon.Handle
                    }
                    weapon.Combo.Kie:FireServer(unpack(args))
                else
                    warn(weaponName .. " not found in character!")
                end
            end
        end
    end)

    -- รีเซ็ตเมื่อผู้เล่นตาย
    deathEvent = humanoid.Died:Connect(function()
        if Toggle.Value then
            print("Player has died. Resetting...")
            player.CharacterAdded:Wait()
            setupCharacter(player.Character)
        end
    end)
end

-- เช็คว่า Toggle เปิดหรือปิด
Toggle:OnChanged(function(isEnabled)
    if isEnabled then
        -- เริ่มต้นการทำงานเมื่อ Toggle เปิด
        if player.Character then
            setupCharacter(player.Character)
        end
        player.CharacterAdded:Connect(setupCharacter)
    else
        -- ยกเลิกการเชื่อมต่อ Event เมื่อ Toggle ปิด
        if inputEvent then inputEvent:Disconnect() end
        if deathEvent then deathEvent:Disconnect() end
    end
end)

local Toggle = Tabs.Weapon:AddToggle("MyToggle", {Title = "Pool_Red", Default = false })



local UserInputService = game:GetService("UserInputService")
local Players = game:GetService("Players")
local player = Players.LocalPlayer

-- เก็บข้อมูลเพื่อจัดการการเชื่อมต่อ Event
local inputEvent
local deathEvent

-- ฟังก์ชันสำหรับโหลด Animation
local function loadAnimation(humanoid)
    local animationId = "rbxassetid://122516524039190"
    local animation = Instance.new("Animation")
    animation.AnimationId = animationId
    local animator = humanoid:FindFirstChild("Animator") or humanoid:WaitForChild("Animator")
    return animator:LoadAnimation(animation)
end

-- ฟังก์ชันหลักที่ทำงานเมื่อ Toggle เปิด
local function setupCharacter(character)
    local humanoid = character:WaitForChild("Humanoid")
    local animationTrack = loadAnimation(humanoid)

    -- เชื่อมต่อเมื่อกดปุ่ม Q
    inputEvent = UserInputService.InputBegan:Connect(function(input, gameProcessed)
        if Toggle.Value and not gameProcessed and input.KeyCode == Enum.KeyCode.Q then
            -- รันท่าทาง
            animationTrack:Play()

            -- รันคำสั่ง for-loop
            for i = 1, 6 do
                local weaponName = "Pool_RedUpgrade" .. i
                local weapon = character:FindFirstChild(weaponName)

                if weapon then
                    local args = {
                        [1] = weapon.Handle
                    }
                    weapon.Combo.Kie:FireServer(unpack(args))
                else
                    warn(weaponName .. " not found in character!")
                end
            end
        end
    end)

    -- รีเซ็ตเมื่อผู้เล่นตาย
    deathEvent = humanoid.Died:Connect(function()
        if Toggle.Value then
            print("Player has died. Resetting...")
            player.CharacterAdded:Wait()
            setupCharacter(player.Character)
        end
    end)
end

-- เช็คว่า Toggle เปิดหรือปิด
Toggle:OnChanged(function(isEnabled)
    if isEnabled then
        -- เริ่มต้นการทำงานเมื่อ Toggle เปิด
        if player.Character then
            setupCharacter(player.Character)
        end
        player.CharacterAdded:Connect(setupCharacter)
    else
        -- ยกเลิกการเชื่อมต่อ Event เมื่อ Toggle ปิด
        if inputEvent then inputEvent:Disconnect() end
        if deathEvent then deathEvent:Disconnect() end
    end
end)



local Toggle = Tabs.Weapon:AddToggle("MyToggle", {Title = "Boreas_Sword", Default = false })



local UserInputService = game:GetService("UserInputService")
local Players = game:GetService("Players")
local player = Players.LocalPlayer

-- เก็บข้อมูลเพื่อจัดการการเชื่อมต่อ Event
local inputEvent
local deathEvent

-- ฟังก์ชันสำหรับโหลด Animation
local function loadAnimation(humanoid)
    local animationId = "rbxassetid://122516524039190"
    local animation = Instance.new("Animation")
    animation.AnimationId = animationId
    local animator = humanoid:FindFirstChild("Animator") or humanoid:WaitForChild("Animator")
    return animator:LoadAnimation(animation)
end

-- ฟังก์ชันหลักที่ทำงานเมื่อ Toggle เปิด
local function setupCharacter(character)
    local humanoid = character:WaitForChild("Humanoid")
    local animationTrack = loadAnimation(humanoid)

    -- เชื่อมต่อเมื่อกดปุ่ม Q
    inputEvent = UserInputService.InputBegan:Connect(function(input, gameProcessed)
        if Toggle.Value and not gameProcessed and input.KeyCode == Enum.KeyCode.Q then
            -- รันท่าทาง
            animationTrack:Play()

            -- รันคำสั่ง for-loop
            for i = 1, 6 do
                local weaponName = "Boreas_Sword" .. i
                local weapon = character:FindFirstChild(weaponName)

                if weapon then
                    local args = {
                        [1] = weapon.Handle
                    }
                    weapon.Combo.Kie:FireServer(unpack(args))
                else
                    warn(weaponName .. " not found in character!")
                end
            end
        end
    end)

    -- รีเซ็ตเมื่อผู้เล่นตาย
    deathEvent = humanoid.Died:Connect(function()
        if Toggle.Value then
            print("Player has died. Resetting...")
            player.CharacterAdded:Wait()
            setupCharacter(player.Character)
        end
    end)
end

-- เช็คว่า Toggle เปิดหรือปิด
Toggle:OnChanged(function(isEnabled)
    if isEnabled then
        -- เริ่มต้นการทำงานเมื่อ Toggle เปิด
        if player.Character then
            setupCharacter(player.Character)
        end
        player.CharacterAdded:Connect(setupCharacter)
    else
        -- ยกเลิกการเชื่อมต่อ Event เมื่อ Toggle ปิด
        if inputEvent then inputEvent:Disconnect() end
        if deathEvent then deathEvent:Disconnect() end
    end
end)

Tabs.Weapon:AddParagraph({
        Title = "---------------------------------------- AimBot ↓ ----------------------------------",
        Content = ""
    })

local Toggle = Tabs.Weapon:AddToggle("MyToggle", {Title = "AimBot", Default = false })

local ScreenGui -- ตัวแปรสำหรับเก็บอ้างอิง UI
local FOVCircle -- ตัวแปรสำหรับเก็บอ้างอิงวงกลม FOV
local PlusSign -- ตัวแปรสำหรับเก็บอ้างอิงป้าย + 
local ClosestPlayer = nil
local ShortestDistance = math.huge
local FOV = math.rad(25) -- Define FOV in radians
local isEnabled = false  -- ตัวแปรสำหรับเก็บสถานะเปิด/ปิด
local findPlayerConnection -- ตัวแปรเก็บการเชื่อมต่อของฟังก์ชันค้นหาผู้เล่น
local rotateConnection -- ตัวแปรเก็บการเชื่อมต่อของฟังก์ชันหมุนกล้อง

Toggle:OnChanged(function(state)
    isEnabled = state  -- อัปเดตสถานะเมื่อ Toggle เปลี่ยนแปลง

    local Players = game:GetService("Players")
    local LocalPlayer = Players.LocalPlayer
    local Camera = workspace.CurrentCamera

    -- หากเปิด Toggle จะสร้าง UI และฟังก์ชันทั้งหมด
    if isEnabled then
        -- Create a UI element to show FOV
        ScreenGui = Instance.new("ScreenGui")
        ScreenGui.Parent = LocalPlayer.PlayerGui

        -- Create a Frame to represent the FOV (only the border)
        FOVCircle = Instance.new("Frame")
        FOVCircle.Size = UDim2.new(0, 200, 0, 200) -- Adjust size as needed
        FOVCircle.Position = UDim2.new(0.5, -70, 0.5, -100) -- Centered with a slight shift to the right
        FOVCircle.BackgroundTransparency = 1 -- Make background transparent
        FOVCircle.BorderSizePixel = 0 -- Remove border thickness from the Frame
        FOVCircle.Parent = ScreenGui

        -- Make the Frame circular
        local UICorner = Instance.new("UICorner")
        UICorner.CornerRadius = UDim.new(0.5, 0) -- This makes it a circle
        UICorner.Parent = FOVCircle

        -- Add a UIStroke to create a border with the smallest possible thickness
        local UIStroke = Instance.new("UIStroke")
        UIStroke.Parent = FOVCircle
        UIStroke.Thickness = 0.5 -- Set the thickness to the smallest value
        UIStroke.Color = Color3.fromRGB(255, 0, 0) -- Red color for the border
        UIStroke.ApplyStrokeMode = Enum.ApplyStrokeMode.Border

        -- Create a TextLabel for the + symbol at the center of the circle
        PlusSign = Instance.new("TextLabel")
        PlusSign.Size = UDim2.new(0, 12, 0, 12) -- Make the + symbol even smaller
        PlusSign.Position = UDim2.new(0.5, -6, 0.5, -6) -- Position the + in the center of the circle
        PlusSign.Text = "+"
        PlusSign.TextSize = 8 -- Make the text size even smaller
        PlusSign.TextColor3 = Color3.fromRGB(255, 0, 0) -- Red color for the + symbol
        PlusSign.BackgroundTransparency = 1 -- Make the background transparent
        PlusSign.TextStrokeTransparency = 0.8 -- Optional: Add stroke effect to make the text stand out
        PlusSign.Parent = FOVCircle

        -- Function to find the closest player within FOV
        local function findClosestPlayer()
            ClosestPlayer = nil
            ShortestDistance = math.huge

            for _, player in pairs(Players:GetPlayers()) do
                if player ~= LocalPlayer and player.Character and player.Character:FindFirstChild("HumanoidRootPart") then
                    local targetPosition = player.Character.HumanoidRootPart.Position
                    local cameraPosition = Camera.CFrame.Position
                    local directionToTarget = (targetPosition - cameraPosition).Unit
                    local cameraLookVector = Camera.CFrame.LookVector

                    -- Check if the player is within the FOV
                    local angle = math.acos(cameraLookVector:Dot(directionToTarget))
                    if angle <= FOV then
                        -- Calculate distance to find the closest player within the FOV
                        local distance = (cameraPosition - targetPosition).Magnitude
                        if distance < ShortestDistance then
                            ShortestDistance = distance
                            ClosestPlayer = player
                        end
                    end
                end
            end
        end

        -- Function to update the FOV display (show only the circular border)
        local function updateFOVDisplay()
            -- Adjust the FOV circle to reflect changes in the player's view direction
            local cameraFov = Camera.FieldOfView
            local size = math.clamp(cameraFov / 100, 0.2, 1) * 200 -- Dynamically adjust the size of the circle based on the camera FOV
            FOVCircle.Size = UDim2.new(0, size, 0, size)
        end

        -- Function to smoothly rotate camera towards the head of the closest player
        local function rotateCameraTowardsPlayer(player)
            if player.Character and player.Character:FindFirstChild("Head") then
                local playerHeadPosition = player.Character.Head.Position
                local cameraPosition = Camera.CFrame.Position
                local directionToPlayerHead = (playerHeadPosition - cameraPosition).Unit

                -- Create a new CFrame that looks at the player's head position
                local targetCFrame = CFrame.new(cameraPosition, playerHeadPosition)

                -- Smoothly rotate the camera towards the player's head
                Camera.CFrame = Camera.CFrame:Lerp(targetCFrame, 0.1)
            end
        end

        -- Update the FOV display every frame
        findPlayerConnection = game:GetService("RunService").RenderStepped:Connect(updateFOVDisplay)

        -- Update the closest player within FOV every frame
        rotateConnection = game:GetService("RunService").RenderStepped:Connect(function()
            findClosestPlayer()  -- Find the closest player in FOV
            if ClosestPlayer then
                -- Rotate camera towards the closest player's head smoothly
                rotateCameraTowardsPlayer(ClosestPlayer)
            end
        end)

    else
        -- เมื่อปิด Toggle ลบ UI และเคลียร์ค่าภายใน
        if ScreenGui then
            ScreenGui:Destroy()  -- ลบ UI ทั้งหมด
            ScreenGui = nil
        end
        ClosestPlayer = nil
        ShortestDistance = math.huge
        
        -- ปิดการเชื่อมต่อและหยุดการทำงานของฟังก์ชัน
        if findPlayerConnection then
            findPlayerConnection:Disconnect()
            findPlayerConnection = nil
        end

        if rotateConnection then
            rotateConnection:Disconnect()
            rotateConnection = nil
        end
    end
end)

Tabs.Weapon:AddParagraph({
        Title = "---------------------------------------- Risk ↓ --------------------------------",
        Content = ""
    })

local Toggle = Tabs.Weapon:AddToggle("MyToggle", {Title = "Bomb fist", Default = false})
local UserInputService = game:GetService("UserInputService")

local isToggleActive = false  -- ตัวแปรสำหรับเก็บสถานะของ Toggle
local connection  -- ตัวแปรเก็บการเชื่อมต่อ InputBegan

-- ฟังก์ชันในการฟังการกดปุ่ม Q
local function onQPress(input, gameProcessed)
    if input.KeyCode == Enum.KeyCode.Q and not gameProcessed and isToggleActive then
        -- เริ่มการทำงานเมื่อกดปุ่ม "Q" และ Toggle เปิดใช้งาน
        local player = game.Players.LocalPlayer
        local character = player.Character or player.CharacterAdded:Wait()
        local humanoidRootPart = character:WaitForChild("HumanoidRootPart")

        -- ส่วนของการย้าย object
        local targetPart = workspace.MAPFOUR["1"]

        if targetPart then
            -- บันทึกตำแหน่งเดิมของ object
            local originalPosition = targetPart.CFrame

            -- ย้าย object มาที่ตำแหน่งของผู้เล่น
            targetPart.CFrame = humanoidRootPart.CFrame

            -- รอ 3 วินาที
            task.wait(0)

            -- ย้าย object กลับไปยังตำแหน่งเดิม
            targetPart.CFrame = originalPosition
        else
            warn("ไม่พบ object '1' ใน workspace.MAPFOUR")
        end

        -- ตั้งค่าผู้เล่นให้ตาย
        if character:FindFirstChild("Humanoid") then
            character.Humanoid.Health = 0
        end

        -- เรียกใช้งานการชุบชีวิต
        local reviveEvent = game:GetService("ReplicatedStorage"):WaitForChild("ReviveSystem"):WaitForChild("Event")

        local respawnPosition = humanoidRootPart.Position  -- บันทึกตำแหน่งที่รันสคริปต์
wait(0.5)
        local args = {
            [1] = "Respawn",
            [2] = player
        }

        -- เรียกใช้คำสั่ง respawn
        reviveEvent:FireServer(unpack(args))

        -- รอให้ respawn เสร็จ
        player.CharacterAdded:Wait()

        -- รอให้การ respawn เสร็จสมบูรณ์
        task.wait(0.7)

        -- วาบกลับไปยังตำแหน่งเดิมหลังจาก respawn เสร็จ
        player.Character.HumanoidRootPart.CFrame = CFrame.new(respawnPosition)
    end
end

-- เมื่อ Toggle เปลี่ยนแปลง
Toggle:OnChanged(function(value)
    isToggleActive = value  -- เก็บสถานะของ Toggle

    -- หาก Toggle เปิดให้เชื่อมต่อฟังก์ชัน InputBegan
    if isToggleActive then
        if not connection then  -- ถ้ายังไม่ได้เชื่อมต่อ
            connection = UserInputService.InputBegan:Connect(onQPress)
        end
    else
        -- หยุดการฟังการกดปุ่ม Q เมื่อ Toggle ปิด
        if connection then
            connection:Disconnect()
            connection = nil
        end
    end
end)


    Tabs.Weapon:AddButton({
        Title = "load bomb",
        Description = "Click to tp",
        Callback = function()
            Window:Dialog({
                Title = "Title",
                Content = "This is a dialog",
                Buttons = {
                    {
                        Title = "Confirm",
                        Callback = function()
                            local originalPosition = game.Players.LocalPlayer.Character.HumanoidRootPart.Position
local targetPosition = Vector3.new(2188, 22, -2113)

-- วาบไปยังตำแหน่งที่ระบุ
game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(targetPosition)

-- รอ 2 วินาที (หรือระยะเวลาที่ต้องการ) แล้ววาบกลับ
wait(0.2)

-- วาบกลับไปยังตำแหน่งเดิม
game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(originalPosition)

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



        gui:Destroy()
    else
        player:Kick("Invalid key!")
    end
end

submit.MouseButton1Click:Connect(submitKey)
textBox.FocusLost:Connect(function(enterPressed) if enterPressed then submitKey() end end)
