-- updater.lua (SERVER-SIDE)
local CURRENT_VERSION = "1.0.0"
local GITHUB_REPO = "rmdark/keymaster"

AddEventHandler('onResourceStart', function(resourceName)
    if GetCurrentResourceName() ~= resourceName then return end
    
    PerformHttpRequest(("https://api.github.com/repos/%s/releases/latest"):format(GITHUB_REPO), 
    function(err, response, headers)
        if err ~= 200 then
            print(("[^3Keymaster^7] Failed to check updates (Error %s)"):format(err))
            return
        end

        local data = json.decode(response)
        if not data or not data.tag_name then
            print("[^3Keymaster^7] Invalid update response from GitHub")
            return
        end

        local latestVersion = data.tag_name:gsub("v", "")
        if latestVersion ~= CURRENT_VERSION then
            print(("
^5===============================================^7"))
            print(("[^3Keymaster^7] Update available: ^2%s^7 (Current: ^1%s^7)"):format(data.tag_name, "v"..CURRENT_VERSION))
            print(("[^3Keymaster^7] Changelog: ^5%s^7"):format(data.body:gsub("
", " ")))
            print(("[^3Keymaster^7] Download: ^3%s^7"):format(data.html_url))
            print("^5===============================================^7
")
        else
            print("[^3Keymaster^7] Resource is ^2up to date^7")
        end
    end, 'GET', '', {}, {code = 200})
end)
