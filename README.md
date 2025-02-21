local resourceFolder = "keymaster"
local currentVersionFile = resourceFolder .. "/version.txt"
local remoteVersionUrl = "https://raw.githubusercontent.com/rmdark/RichMill-Weapon-Pack-V1/master/version.txt"
local zipUrl = "https://github.com/rmdark/RichMill-Weapon-Pack-V1/archive/refs/tags/1.2.3.zip"
local tempZipPath = resourceFolder .. "/temp.zip"
local tempExtractPath = resourceFolder .. "/temp_extract"

-- Function to read a file synchronously
local function readFile(filePath)
    local file = io.open(filePath, "r")
    if not file then return nil end
    local content = file:read("*a")
    file:close()
    return content
end

-- Function to write a file synchronously
local function writeFile(filePath, content)
    local file = io.open(filePath, "w")
    if file then
        file:write(content)
        file:close()
    end
end

-- Function to download a file
local function downloadFile(url, filePath)
    PerformHttpRequest(url, function(statusCode, response, headers)
        if statusCode == 200 then
            print("Download successful.")
            writeFile(filePath, response)
        else
            print("Download failed with status code: " .. statusCode)
        end
    end)
end

-- Function to extract a zip file
local function extractZip(zipPath, extractPath)
    -- Using a basic shell command to extract zip, assuming you use unzip utility
    -- You can use a Lua library for better cross-platform support
    os.execute("unzip " .. zipPath .. " -d " .. extractPath)
end

-- Function to check for updates
local function checkForUpdates()
    local currentVersion = readFile(currentVersionFile)
    downloadFile(remoteVersionUrl, tempZipPath)
