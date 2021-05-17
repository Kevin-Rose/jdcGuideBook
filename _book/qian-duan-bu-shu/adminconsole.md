##### npm install 总是失败？

##### 由于中国墙的的原因，安装一些依赖时很容易出现超时问题，国内用户推荐使用淘宝源的安装方式

npm install --registry=[https://registry.npm.taobao.org](https://registry.npm.taobao.org)



    C:\J2EE\SVN\bus-admin-web>npm install
    npm WARN extract-text-webpack-plugin@3.0.2 requires a peer of webpack@^3.1.0 but none is installed. You must install peer dependencies yourself.
    npm WARN script-ext-html-webpack-plugin@2.0.1 requires a peer of html-webpack-plugin@^3.0.0 but none is installed. You must install peer dependencies yourself.
    npm WARN optional SKIPPING OPTIONAL DEPENDENCY: fsevents@1.2.4 (node_modules\fsevents):
    npm WARN notsup SKIPPING OPTIONAL DEPENDENCY: Unsupported platform for fsevents@1.2.4: wanted {"os":"darwin","arch":"any"} (current: {"os":"win32","arch":"x64"})

    removed 11 packages and audited 16843 packages in 26.084s
    found 860 vulnerabilities (453 low, 19 moderate, 388 high)
      run `npm audit fix` to fix them, or `npm audit` for details



