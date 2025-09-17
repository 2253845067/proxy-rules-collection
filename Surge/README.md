# Surge 自用配置

## Sub-Store快捷脚本

**适用于Surge_Rabbit-Spec.conf**

```js
// Sub-Store【快捷脚本】
// 功能：只修改「✈️ 我的节点」行 → policy-path 写死指定链接 + update-interval=86400
// 环境：快捷脚本（有全局 $content，无 export/module/$done）

(() => {
  const LINK = "订阅链接"; // ← 改成你的订阅链接

  try {
    if (typeof $content !== "string" || !$content.length) return;

    const lines = $content.split(/\r?\n/);
    const hit = /^\s*✈️\s*我的节点\s*=/u; // 匹配「✈️ 我的节点 = ...」

    const out = lines.map((line) => {
      if (!hit.test(line)) return line;

      // Step1: 替换或插入 policy-path
      let newLine;
      if (/policy-path\s*=/.test(line)) {
        newLine = line.replace(
          /(policy-path\s*=\s*)([^,\r\n]*)/i,
          (_, p1) => `${p1}${LINK}`
        );
      } else {
        newLine = line.replace(
          /(=\s*[^,]+,)(\s*)/,
          (_, p1, sp) => `${p1}${sp}policy-path=${LINK}, `
        );
      }

      // Step2: 替换或插入 update-interval=86400
      if (/update-interval\s*=/.test(newLine)) {
        newLine = newLine.replace(
          /(update-interval\s*=\s*)(\d+)/i,
          (_, p1) => `${p1}86400`
        );
      } else {
        newLine += ", update-interval=86400";
      }

      return newLine;
    });

    $content = out.join("\n");
  } catch (e) {
    // 出错则保持原始内容
  }
})();

```



**适用于Surge_ACL4SSR.conf**

```js
// Sub-Store【快捷脚本】
// 功能：只修改「✈️ 我的节点」行 → policy-path 写死指定链接 + update-interval=86400
// 环境：快捷脚本（有全局 $content，无 export/module/$done）

(() => {
  const LINK = "订阅链接"; // ← 改成你的订阅链接

  try {
    if (typeof $content !== "string" || !$content.length) return;

    const lines = $content.split(/\r?\n/);
    const hit = /^\s*🚀\s*手动切换\s*=/u; // 匹配「🚀 手动切换 = ...」

    const out = lines.map((line) => {
      if (!hit.test(line)) return line;

      // Step1: 替换或插入 policy-path
      let newLine;
      if (/policy-path\s*=/.test(line)) {
        newLine = line.replace(
          /(policy-path\s*=\s*)([^,\r\n]*)/i,
          (_, p1) => `${p1}${LINK}`
        );
      } else {
        newLine = line.replace(
          /(=\s*[^,]+,)(\s*)/,
          (_, p1, sp) => `${p1}${sp}policy-path=${LINK}, `
        );
      }

      // Step2: 替换或插入 update-interval=86400
      if (/update-interval\s*=/.test(newLine)) {
        newLine = newLine.replace(
          /(update-interval\s*=\s*)(\d+)/i,
          (_, p1) => `${p1}86400`
        );
      } else {
        newLine += ", update-interval=86400";
      }

      return newLine;
    });

    $content = out.join("\n");
  } catch (e) {
    // 出错则保持原始内容
  }
})();

```

