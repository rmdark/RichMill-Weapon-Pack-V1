local GH_REPO = "rmdark/RichMill-Weapon-Pack-V1"

AddEventHandler('onResourceStart', function(resource)
if GetCurrentResourceName() ~= resource then return end

print("
^5---------------------------------------")
print("Checking for Rm Weapon Pack updates...")
print("Current Version: ^2"..GetResourceMetadata(resource, 'version').."^5")

PerformHttpRequest(("https://api.github.com/repos/%s/releases/latest"):format(GH_REPO),
function(err, text, headers)
if err == 200 then
local data = json.decode(text)
if data.tag_name ~= GetResourceMetadata(resource, 'version') then
print("Update Available: ^1"..data.tag_name.."^5")
print("Download: ^3"..data.html_url.."^5")
end
print("---------------------------------------^0
")
end
end)
end)
local RM_WEAPONPACK_VERSION = "v1.0.0"
Citizen.CreateThread(function()
print([[
[36m
█▀█ █▀▄▀█   █ █ █ █▀▀ ▄▀█ █▀█ █▀█ █▄ █   █▀█ ▄▀█ █▀▀ █▄▀
█▀▄ █ ▀ █   ▀▄▀▄▀ ██▄ █▀█ █▀▀ █▄█ █ ▀█   █▀▀ █▀█ █▄▄ █ █]])
print("^5RM Weapon Pack "..RM_WEAPONPACK_VERSION.."^0 - ^2Successfully loaded!
^7")
end)
