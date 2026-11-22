# FFXI Addon — FuckOff

> [!NOTE]
> **Quick Reference**
> - **Path:** `C:\Windower\addons\FuckOff\`
> - **Author / Version:** Chiaia (Asura) / `0.10`
> - **Commands:** `//fuckoff`, `//fo` *(declared in `_addon.commands`, no command handler implemented)*
> - **Load Status:** `scripts/init.txt`
> - **Origin:** Third-Party

Lightweight incoming-chat packet filter that silently drops RMT/mercenary spam and blacklisted senders before messages reach the chat log.

## What the Code Does
`FuckOff.lua` listens to `incoming chunk` for packet `0x017` (incoming chat). After parsing the packet and normalizing auto-translate tags (`windower.convert_auto_trans(chat['Message']):lower()`):
1. If `chat['Sender Name']` is in `blackListedUsers`, returns `true` to block the packet in **any** chat mode.
2. Otherwise, if `chat['Mode']` is `3` (Tell), `1` (Say), or `26` (Yell), iterates `blackListedWords` (`☆`/`★` Shift-JIS bytes `0x81 0x99` / `0x81 0x9A`, `1-99`, `Job Point.*2100`, `500p`, `1M/1hour`, `/hr`, `Discount`, etc.) and returns `true` on the first pattern match to suppress the message.

## Commands & Usage
No runtime commands are implemented; customization is done by editing `blackListedUsers` and `blackListedWords` in `FuckOff.lua`.

## Events, Packets & Technical Hooks
- **Windower Events:** `incoming chunk`
- **Packets:** Incoming `0x017` (chat message — blocks by returning `true`)
- **Dependencies / Libraries:** `packets`

## Local Settings & Customizations
No `data/settings.xml`. `blackListedUsers` in `FuckOff.lua` contains `TotallyABotOne`, `TotallyABotTwo`, `TotallyABotThree`, and `Kimaxaxaxa`.

## Related Notes
- `FFXI Windower Overview`
- `FFXI Windower Addons Catalog`
