# SC:R BWAPI Bridge Launcher

## 中文

**仅保证对 StarCraft Remastered 1.23.10.13515 x86 的支持。** 普通启动不再校验游戏主程序的 SHA-256，也不按版本号阻止其他 x86 客户端启动。其他版本可以尝试，但地址布局和原生函数可能不同，尚未验证；取消校验不代表已经适配这些版本。BOT练习模式单独限定为已验证的 13515 x86 客户端。x64 游戏和 x64 bot 不受支持。

### 内容与运行环境

- `BWAPI-Bridge-Launcher.exe`：中英文图形启动器，已内置桥接代理和运行库，无需项目源码、PowerShell 脚本或编译工具。
- `AIModule/`、`AIClientModule/`：从项目原样复制的完整 bot 文件夹，包括依赖、配置和客户端兼容配置。
- `bot-versions.ini`：按名称、入口文件、类型匹配 BWAPI 版本的名单；仅允许登记为 4.4.0 的 bot。不使用 bot 文件 SHA 来判定版本。
- `licenses/`：第三方组件许可证及说明。
- 启动器使用原生 C++/Win32，静态链接 C/C++ 运行库，不需要 .NET 或单独安装启动器运行库。支持 Windows 10/11。桥接运行时和各 bot 仍可能需要 Microsoft Visual C++ **x86** 运行库；保留其附带依赖。
- 不包含 StarCraft 游戏文件。请使用自己的游戏安装目录，并将整个发布文件夹解压到可写位置。

### 使用

1. 双击 `BWAPI-Bridge-Launcher.exe`。右上角可在“简体中文 / English”之间切换，选择会保存。
2. 点击“选择游戏…”，选择游戏安装目录 `x86/StarCraft.exe`。
3. 选择 bot。默认列表包含 `AIModule` 的 DLL 及 `AIClientModule` 的 EXE；也可选择其他目录或直接选择 DLL / EXE。地图和种族请按 bot 要求手动选择。
4. 点击“启动游戏”。启动器先备份原始 SDK、安装桥接、配置 bot 和分发 JSON，再启动游戏。更换 bot 或更新桥接前先正常关闭游戏。
5. 在游戏中进入单人模式或 UDP 局域网房间。EXE 客户端由桥接自动启动；无需手动另开。客户端若要求管理员权限，启动器会请求 Windows UAC 授权，请自行确认。

### BOT练习模式

1. 选择 bot 和游戏，勾选“BOT练习模式”，确认界面显示其 SCHNAIL 种族标记：`P` 神族、`T` 人族、`Z` 虫族、`R` 随机。可先选择 Stardust DLL，应显示 `P`。种族名单包含 87 个标记；缺少或无效标记会阻止练习模式启动，不默认随机。默认不勾选此模式。
2. 点击“启动游戏”，在玩家窗口手动进入多人游戏、UDP 并创建房间。启动器识别实际房间名后，才启动独立桌面中的后台机器人，自动加入该房间并请求所选种族。首次加入失败会自动重试，总共最多三次。
3. 等待“机器人已就绪，等待玩家开局”，再由玩家手动开始游戏。玩家端禁用 bot，保留自己的显示设置；机器人端加载所选 bot，使用会话内独立的标清、窗口模式配置，不覆盖玩家的 `CSettings.json`。
4. 练习时保持启动器打开。玩家退出或关闭启动器时，会清理后台机器人及其 CEF/客户端子进程；关闭启动器不会结束玩家游戏。
5. 玩家正常结束、认输或退出对局后，启动器根据玩家完成轮次回收后台机器人，显示等待新房间，不等待机器人自行离开胜利页。玩家可继续创建同名或其他名称的 UDP 房间，机器人会重新启动并加入，玩家无需退出游戏。

每次会话的配置与日志分别保存在 `%LOCALAPPDATA%/SCR-BWAPI-Bridge-Launcher/duels/<会话 ID>/player` 和 `bot` 中。“打开日志目录”指向机器人端目录；玩家端目录与其相邻。游戏本体不复制，端口配置不写入注册表。

机器人单独使用 `--noSound` 参数，玩家端声音设置保持原样。机器人窗口位于独立 Win32 桌面，内部渲染和 CEF 菜单循环仍然保留，不是跳过图形引擎的无渲染实现。

此前可见窗口流程已通过 Stardust 自动入房、选族和用户开局后的回调验证。**本次独立标清/窗口设置及连续开局的真实游戏效果仍待用户验收**。机器人 `bridge.log` 中的 `bot CSettings.json read redirected` 可确认读取了独立配置；仅有安装钩子的日志不能证明启动时实际读取成功。自动辅助程序测试不能替代游戏验收。非 ASCII 房间名也尚未完成真实验证。

### 支持范围与配置

- 支持 BWAPI 4.4.0 x86 DLL 模块和 EXE 客户端；属于实验性兼容桥接，并非完整替代 BWAPI 4.4.0 / Brood War 1.16.1。名单中的版本声明也不等于所有 bot 均已实战验证。
- 单人模式支持 debug 绘制及原生 `printf`、`sendText`、`sendTextEx` 输出。bot 自身必须发出相应绘制或文字指令才会显示。
- UDP 局域网保留 debug 绘制，禁用 bot 调速。Battle.net、主菜单 Login 和 Purchase Now 入口均已拦截。
- BWAPI 4.1.x 和 x64（包括 PurpleWave）的适配暂未纳入发布支持范围。
- 两个 bot 目录按要求完整保留。`krasi0` 和 `Moster2025` 已按项目实测结果登记为 4.4.0，允许启动；`tscmoo` 仍登记为 4.1.2，会被校验拦截。
- EXE 的版本名单与 IPC 协议号分别处理。启动器读取其 `.exe.bridge-client.ini` 中的 `ClientVersion`，保留 Krasi0、Monster 所需的 `10002`；无配置时默认 `10003`。
- 启动时部署所选 bot 的 JSON、DAT、BIN 模型、CSV、采矿 TXT 和 BWTA2 缓存，保留规范 AI/read/BWTA2 目录。模块使用游戏工作目录；EXE 客户端也会准备自身目录。krasi0 的旧版安装目录查找会单独补地形数据，不修改注册表。
- 原有 `read` 对手数据不会被覆盖；不同的旧配置/静态资源先备份到 `bwapi-data/bridge-config-backups`。`write` 数据不会导入。Odin 缺模型、Monster 缺 sc.dat 会在启动前报错；原包未附带的任意配置和在线服务仍需单独检查。
- 新增 bot 需在 `bot-versions.ini` 登记对应的节名、`BotExecutable`、`BotType=DLL` 或 `CLIENT_EXE`、`Version=4.4.0`；练习模式另需按 SCHNAIL 登记 `Race=P/T/Z/R`。填写声明不会把旧版 bot 转换为 4.4.0。

### 文件、日志与恢复

桥接写入所选游戏的 `x86` 目录：`ClientSdk.dll`、`BridgeRuntime.dll`、`bridge.ini`、`bot-versions.ini` 和安装记录 `bridge.install.json`。原始 SDK 保留为 `ClientSdkOriginal.dll`，请勿删除或替换。安装记录中的哈希仅用于保护备份及已安装文件，不用于限制游戏版本。

日志位于同一目录：`bridge.log`、`bridge-runtime.log`、`bridge-events.jsonl`；可点击“打开日志目录”。设置位于 `%LOCALAPPDATA%/SCR-BWAPI-Bridge-Launcher/settings.json`。游戏目录需要写入权限；若位于受保护位置，可右键以管理员身份运行启动器。

恢复原始游戏：正常关闭游戏与启动器，将 `x86/ClientSdkOriginal.dll` **复制并覆盖** `x86/ClientSdk.dll`，保留原始备份。此后不通过桥接启动器启动游戏；再次点击桥接的“启动游戏”会重新安装代理。恢复 SDK 后，可保留其余桥接日志和配置，不影响原始 SDK 加载。

## English

**Support is guaranteed only for StarCraft Remastered 1.23.10.13515 x86.** Normal launches do not check the game executable's SHA-256 or block other x86 clients by version number. Other versions may be tried, but their memory layouts and native functions may differ and remain unverified. Removing the gate does not establish compatibility. BOT Practice Mode separately requires the verified 13515 x86 client. x64 games and bots are unsupported.

### Contents and requirements

- `BWAPI-Bridge-Launcher.exe`: Chinese/English GUI with the proxy and bridge runtime embedded. No project source, PowerShell scripts or build tools are required.
- `AIModule/` and `AIClientModule/`: complete, unchanged copies of the project's bot folders, including dependencies, configurations and client profiles.
- `bot-versions.ini`: a name, entry filename and type catalog. Only bots declared as BWAPI 4.4.0 are allowed. Bot hashes are not used to identify BWAPI versions.
- `licenses/`: third-party component licenses and notices.
- Native C++/Win32 launcher with a statically linked C/C++ runtime; no .NET or separate launcher runtime installation is required. Supports Windows 10/11. The bridge runtime and bots may still need Microsoft Visual C++ **x86** runtimes; retain supplied dependencies.
- StarCraft game files are not included. Use your own installation and extract the complete release folder to a writable location.

### Launching

1. Open `BWAPI-Bridge-Launcher.exe`. Select “简体中文 / English” at the top right; the preference is saved.
2. Click “Browse game…” and select `x86/StarCraft.exe` in your game installation.
3. Select a bot. The default list includes module DLLs from `AIModule` and client EXEs from `AIClientModule`. You can browse another folder or select an individual DLL / EXE. Choose the map and race required by the bot in the game.
4. Click “Launch game”. The launcher backs up the original SDK, installs the bridge, configures the bot and deploys its JSON before starting the game. Close the game normally before changing bots or updating the bridge.
5. Enter single player or a UDP LAN room. The bridge starts standalone EXE clients automatically. If a client requires administrator privileges, the launcher requests Windows UAC approval.

### BOT Practice Mode

1. Select the bot and game, enable “BOT Practice Mode” and check its SCHNAIL race marker: `P` Protoss, `T` Terran, `Z` Zerg or `R` Random. Start with the Stardust DLL, which should show `P`. The catalog includes 87 race markers. Missing or invalid markers block practice mode instead of defaulting to Random. This mode is off by default.
2. Click “Launch game”. In the player window, manually enter multiplayer, select UDP and create a room. Only after detecting its actual name does the launcher start the background bot on a private desktop, automatically join the room and request the selected race. Failed joins are retried automatically, with at most three attempts in total.
3. Wait until the launcher reports that the bot is ready, then start the match manually. The player keeps its display settings with the bot disabled. The background instance loads the selected bot with an independent SD/windowed settings file in its session folder, without overwriting the player's `CSettings.json`.
4. Keep the launcher open during practice. Exiting the player game or closing the launcher cleans up the background bot and its CEF/client children. Closing the launcher leaves the player game running.
5. When the player finishes, surrenders or leaves the match, the launcher stops the background bot and waits for a new room, without waiting for the bot to leave its victory screen. Create another UDP room with the same or a different name to restart the bot and join again. The player game stays open.

Each session keeps separate configuration and logs under `%LOCALAPPDATA%/SCR-BWAPI-Bridge-Launcher/duels/<session ID>/player` and `bot`. “Open log folder” opens the bot directory; the player directory is next to it. The game installation is not duplicated and no port settings are written to the registry.

Only the bot receives `--noSound`; player audio settings remain unchanged. The bot's windows use a private Win32 desktop. Internal rendering and the CEF menu loop remain active; this does not bypass the graphics engine.

The earlier visible-window flow passed Stardust room joining, race selection and callbacks after a user-started match. **Independent SD/windowed settings and repeat matches still require real-game acceptance.** The bot's `bridge.log` reports `bot CSettings.json read redirected` when the independent profile is read; a hook-installation message alone does not establish that startup loaded it. Helper-process tests do not establish actual gameplay behavior. Non-ASCII room names also remain unvalidated in a real session.

### Features and configuration

- Supports BWAPI 4.4.0 x86 module DLLs and client EXEs. This is an experimental compatibility bridge, not a complete replacement for BWAPI 4.4.0 / Brood War 1.16.1. A catalog entry does not mean every bot has been tested in a match.
- Single player supports debug drawing and native `printf`, `sendText` and `sendTextEx` output. The bot must issue the corresponding drawing or text commands.
- UDP LAN retains debug drawing and disables bot speed changes. Battle.net and the main-menu Login and Purchase Now entry points are blocked.
- BWAPI 4.1.x and x64 support, including PurpleWave, are outside this release's support scope.
- Both bot folders are preserved in full as requested. `krasi0` and `Moster2025` are registered as 4.4.0 based on project match verification and are allowed to launch. `tscmoo` remains listed as 4.1.2 and is blocked by version validation.
- The bot version catalog and IPC protocol number are handled separately. The launcher reads `ClientVersion` from `.exe.bridge-client.ini`, preserving `10002` for Krasi0 and Monster. Clients without a profile default to `10003`.
- Startup deploys selected-bot JSON, DAT, BIN models, CSV, mining TXT and BWTA2 caches, preserving canonical AI/read/BWTA2 layouts. Modules use the game working directory; EXE clients also have their own directory prepared. Krasi0 terrain data is also staged to its legacy installation lookup roots without changing the registry.
- Existing opponent `read` data is preserved. Replaced configuration/static resources are backed up under `bwapi-data/bridge-config-backups`; `write` data is not imported. Missing Odin models or Monster sc.dat stop preparation. Unbundled configuration and online services still require separate checks.
- To add a bot, register its section name, `BotExecutable`, `BotType=DLL` or `CLIENT_EXE`, and `Version=4.4.0` in `bot-versions.ini`. Practice mode also requires `Race=P/T/Z/R` from SCHNAIL. Declaring a version does not convert an older bot to 4.4.0.

### Files, logs and restoration

The bridge writes `ClientSdk.dll`, `BridgeRuntime.dll`, `bridge.ini`, `bot-versions.ini` and `bridge.install.json` to the selected game's `x86` directory. The original SDK is preserved as `ClientSdkOriginal.dll`; do not remove or replace it. Installation hashes protect backups and owned files only; they do not restrict game versions.

Logs in that directory are `bridge.log`, `bridge-runtime.log` and `bridge-events.jsonl`. Use “Open log folder” to find them. Settings are stored in `%LOCALAPPDATA%/SCR-BWAPI-Bridge-Launcher/settings.json`. The game directory must be writable; run the launcher as administrator if it is in a protected location.

To restore the original game, close the game and launcher normally, then **copy and overwrite** `x86/ClientSdk.dll` with `x86/ClientSdkOriginal.dll`, retaining the backup. Start the game without the bridge launcher afterward; clicking “Launch game” in the bridge will reinstall its proxy. Other bridge logs and configuration files can remain after restoring the SDK.
