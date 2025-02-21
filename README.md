-- updater.lua
local RESOURCE_NAME = "BuilderJob" -- Replace with your resource name
local CURRENT_VERSION = "1.0.0"
local GITHUB_PATH = "YourGitHub/Repository" -- Change this

print([[
 __                 ___       __   __           __        __       
|__)  |\/|    |  | |__   /\  |__) /  \ |\ |    |__)  /\  /  ` |__/ 
|  \  |  |    |/\| |___ /~~\ |    \__/ | \|    |    /~~\ \__, |  \ 
                                                                   ]].."
"..[[
      Initializing ^5]]..RESOURCE_NAME..[[^7 - Version: ^2v]]..CURRENT_VERSION..[[^7
]])

AddEventHandler('onResourceStart', function(resName)
if GetCurrentResourceName() ~= resName then return end

PerformHttpRequest(("https://api.github.com/repos/%s/releases/latest"):format(GITHUB_PATH),
function(err, response)
if err ~= 200 then return end

local data = json.decode(response)
if not data or not data.tag_name then return end

local latestVersion = data.tag_name:gsub("v", "")
if latestVersion ~= CURRENT_VERSION then
print(("
^3[UPDATE] %s v%s available! Download: ^5%s^0"):format(
RESOURCE_NAME,
data.tag_name,
data.html_url
))
end
end, 'GET')
end)
