# vue3.0使用typescript开发项目总结

## 项目起步

 * 安装ts `npm install -g typescript`
 * 安装vue-cli `npm install -g @vue/cli`
 * 初始化项目 `vue create projectName`
 * 启动 `npm run serve`

## typescript总结

 * 使用`vue.extends` 和`vue-property-decorator`的区别 
   - `vue.extends` 的 `computed` 和 `methods` 有this参与的，必须添加返回值类型声明