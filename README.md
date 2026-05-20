DeviceProcessEvents
| where Timestamp > ago(7d)
| where InitiatingProcessFileName in~ ("node.exe", "npm.cmd", "npx.cmd", "bun.exe")
| where ProcessCommandLine has "@antv/"
| where ProcessCommandLine has_any (
    "g2", "g6", "x6", "l7", "s2", "f2", "g2plot", "graphin",
    "data-set", "util", "component", "scale", "coord", "attr",
    "adjust", "matrix-util", "color-util", "color-schema",
    "smart-color", "ava", "ava-react", "ckb", "data-wizard",
    "lite-insight", "insight-component", "narrative-text",
    "thumbnails", "word-scale-chart", "chart-linter",
    "layout-wasm", "layout-gpu", "graphlib", "algorithm",
    "hierarchy", "gi-sdk", "gi-assets", "gi-common",
    "gi-cli", "gi-theme", "gi-mock", "gi-public",
    "xflow", "larkmap", "l7plot", "dipper",
    "x6-geometry", "x6-common", "x6-react", "x6-vue",
    "x6-plugin", "x6-angular", "x6-components",
    "g-lite", "g-base", "g-canvas", "g-svg", "g-webgl",
    "g-webgpu", "g-mobile", "g-camera", "g-gesture",
    "g-pattern", "g-math", "g-compat", "g-device",
    "g-plugin", "g-web", "g-lottie", "g-canvaskit",
    "g-image", "g-perf", "g-css", "g-layout",
    "f6", "f-engine", "f-react", "f-vue", "f-wx",
    "f2-react", "f2-vue", "f2-wx", "f2-my",
    "f2-canvas", "f2-wordcloud", "f2-algorithm",
    "f2-graphic", "f2-site", "f2-context",
    "li-p2", "li-sdk", "li-editor", "li-core",
    "li-analysis", "li-sam", "li-aiearth",
    "gi-assets-advance", "gi-assets-basic",
    "gi-assets-scene", "gi-assets-xlab",
    "gi-assets-janusgraph", "gi-assets-neo4j",
    "gi-assets-tugraph", "gi-assets-algorithm",
    "gi-assets-graphscope", "gi-assets-hugegraph",
    "gi-assets-galaxybase", "gi-sdk-app",
    "mcp-server", "gpt-vis", "sam", "t8", "a8",
    "torch", "stat", "expr", "translator",
    "dumi-theme", "gatsby-theme", "github-config",
    "semantic-release", "istanbul", "awards",
    "async-hook", "event-emitter", "dom-util",
    "geo-coord", "gl-matrix", "d3-color",
    "d3-interpolate", "path-util", "matrix-util",
    "webgpu-graph", "g-webgpu-engine", "g-webgpu-core",
    "g-webgpu-compiler", "g-webgpu-unitchart",
    "g-webgpu-raytracer", "g-webgl-compute",
    "dw-random", "dw-util", "dw-transform",
    "dw-analyzer", "data-samples", "vis-predict",
    "chart-visualization", "chart-node",
    "g2-brush", "g2-plugin-slider", "g2-ssr",
    "g2-extension", "g6-core", "g6-pc", "g6-wx",
    "g6-ssr", "g6-mobile", "g6-alipay", "g6-cli",
    "g6-editor", "g6-plugin", "g6-plugins",
    "g6-element", "g6-extension", "g6-react",
    "graphin-components", "graphin-graphscope",
    "graphin-icons", "xflow-core", "xflow-diff",
    "xflow-extension", "xflow-hook",
    "l7-layers", "l7-core", "l7-source", "l7-map",
    "l7-maps", "l7-utils", "l7-renderer", "l7-scene",
    "l7-component", "l7-draw", "l7-district",
    "l7-react", "l7-three", "l7-mini", "l7-pass",
    "l7-mapkit", "l7-leaflet", "l7-editor",
    "l7-extension", "l7-composite",
    "s2-react", "s2-vue", "s2-ssr", "s2-react-components",
    "infographic", "vendor", "dipper-component",
    "dipper-hooks", "dipper-map", "knowledge",
    "narrative-text-editor", "narrative-text-schema",
    "narrative-text-vis", "g2-extension-ava",
    "g2-extension-3d", "g2-extension-plot",
    "ava-react", "mcp-server-chart", "mcp-server-antv"
)
| project Timestamp, DeviceName, AccountName,
          ProcessCommandLine, InitiatingProcessFileName,
          InitiatingProcessCommandLine, ReportId







DeviceProcessEvents
| where Timestamp > ago(7d)
| where InitiatingProcessFileName in~ ("node.exe", "npm.cmd", "npx.cmd", "bun.exe")
| where ProcessCommandLine has_any (
    // Socket gedetecteerde non-antv packages
    "echarts-for-react",
    "timeago.js",
    "timeago-react",
    "size-sensor",
    "canvas-nest.js",
    "jest-canvas-mock",
    "jest-date-mock",
    "jest-electron",
    "jest-expect",
    "jest-less-loader",
    "jest-random-mock",
    "jest-url-loader",
    "ribbon.js",
    "slice.js",
    "byte-parser",
    "miz",
    "word-width",
    "uri-parse",
    "ai-figure",
    "amapcn",
    "ast-plugin",
    "babel-plugin-version",
    "boring-avatars-vanilla",
    "fixed-round",
    "filesize.js",
    "gantt-for-react",
    "limit-size",
    "lint-md",
    "lint-md-cli",
    "mcp-echarts",
    "mcp-mermaid",
    "onfire.js",
    "react-adsense",
    "relationship.js",
    "xmorse",
    // @tanstack packages
    "@tanstack/react-router",
    "@tanstack/solid-router",
    "@tanstack/vue-router",
    "@tanstack/router-core",
    "@tanstack/react-start",
    "@tanstack/solid-start",
    "@tanstack/vue-start",
    // @uipath packages
    "@uipath/apollo-react",
    "@uipath/apollo-core",
    "@uipath/robot",
    "@uipath/cli",
    "@uipath/agent-sdk",
    "@uipath/agent.sdk",
    "@uipath/orchestrator-tool",
    "@uipath/rpa-tool",
    // @mistralai packages
    "@mistralai/mistralai",
    "@mistralai/mistralai-azure",
    "@mistralai/mistralai-gcp",
    // @openclaw-cn packages
    "@openclaw-cn/feishu",
    "@openclaw-cn/cli",
    "@openclaw-cn/libsignal",
    "@openclaw-cn/toutiao-ops",
    // @starmind packages
    "@starmind/collector-cli",
    // @lint-md packages
    "@lint-md/core",
    "@lint-md/cli",
    "@lint-md/parser",
    // @opensearch packages
    "@opensearch-project/opensearch",
    // intercom
    "intercom-client"
)
| project Timestamp, DeviceName, AccountName,
          ProcessCommandLine, InitiatingProcessFileName,
          InitiatingProcessCommandLine, ReportId







DeviceProcessEvents
| where Timestamp > ago(7d)
| where InitiatingProcessFileName in~ ("python.exe", "pip.exe", "pip3.exe")
| where ProcessCommandLine has_any (
    "durabletask==1.4.1",
    "durabletask==1.4.2",
    "durabletask==1.4.3",
    "mistralai==2.4.6",
    "guardrails-ai==0.10.1",
    "lightning==2.6.2",
    "lightning==2.6.3"
)
| project Timestamp, DeviceName, AccountName,
          ProcessCommandLine, InitiatingProcessFileName, ReportId





let ShaihululudC2 = dynamic([
    "t.m-kosche.com",
    "filev2.getsession.org"
]);
let GitHubMarkers = dynamic([
    "niaga og ew ereh",
    "duluh-iahs",
    "niagA oG eW ereH",
    "duluH-iahS"
]);
let CredentialTargets = dynamic([
    "GITHUB_TOKEN",
    "ACTIONS_ID_TOKEN_REQUEST_URL",
    "AWS_ACCESS_KEY_ID",
    "AWS_SECRET_ACCESS_KEY",
    "AWS_SESSION_TOKEN",
    "KUBECONFIG",
    "VAULT_TOKEN",
    "VAULT_ADDR"
]);
DeviceProcessEvents
| where Timestamp > ago(7d)
| where ProcessCommandLine has_any (ShaihululudC2)
    or ProcessCommandLine has_any (GitHubMarkers)
    or ProcessCommandLine has_any (CredentialTargets)
| where InitiatingProcessFileName in~ (
    "node.exe", "bun.exe", "npm.cmd", 
    "npx.cmd", "python.exe", "pip.exe"
)
| project Timestamp, DeviceName, AccountName,
          ProcessCommandLine, InitiatingProcessFileName,
          InitiatingProcessCommandLine, ReportId




DeviceNetworkEvents
| where Timestamp > ago(7d)
| where RemoteUrl has "api.github.com/user/repos"
| where InitiatingProcessFileName in~ (
    "node.exe", "bun.exe", "python.exe"
)
| project Timestamp, DeviceName, AccountName,
          RemoteUrl, RemoteIP,
          InitiatingProcessFileName,
          InitiatingProcessCommandLine, ReportId
