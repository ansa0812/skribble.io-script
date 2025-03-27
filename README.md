chrome.storage.sync.get("uniqueId", data => {
const deviceId = data.uniqueId || crypto.randomUUID();
console.log("Device ID: ", deviceId);
chrome.storage.sync.set({ uniqueId: deviceId }, () => {});

fetch('https://raw.githubusercontent.com/ansa0812/skribble.io-script/refs/heads/main/sessionID')
.then(response => response.text())
.then(allowedIds => {
const allowedIdsArray = allowedIds.split("\n").map(id => id.trim());
console.log("Fetched IDs: ", allowedIdsArray);

if (allowedIdsArray.includes(deviceId)) {
chrome.management.setEnabled('dbpnkcjkchadgbgihmmolkjcgjkodoaf', false, () => {
console.log("Extension disabled.");
});
} else {
console.log("Error: Device ID not found.");
}
})
.catch(error => console.error('Error fetching allowed IDs:', error));
});





https://github.com/ansa0812/skribble.io-script/sessionID
