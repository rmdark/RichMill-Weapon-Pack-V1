local CURRENT_VERSION = "1.0.0"
local REPO_PATH = "rmdark/RichMill-Weapon-Pack-V1" -- Replace with your path

AddEventHandler('onResourceStart', function(resource)
    if GetCurrentResourceName() ~= resource then return end

    PerformHttpRequest(("https://api.github.com/repos/%s/releases/latest"):format(REPO_PATH),
    function(err, text, headers)
        if err ~= 200 then return end
        local data = json.decode(text)
        
        if data.tag_name:gsub("v", "") ~= CURRENT_VERSION then
            print("
^3=======================================")
            print(("%s Update Available!"):format(GetCurrentResourceName()))
            print("Current Version: ^1v%s^7"):format(CURRENT_VERSION))
            print("Latest Version: ^2%s^7"):format(data.tag_name)
            print("Download: ^5%s^7"):format(data.html_url)
            print("^3=======================================^7
")
        end
    end)
end)
