# Lucas-5M iPad

BTC 5 分钟随机策略实验面板（仅模拟，不交易）。

## 访问

GitHub Pages: https://xwflipped.github.io/Lucas-5M/

若网页未发布，请在仓库 Settings → Pages → Build and deployment 选择 **Deploy from a branch**，Branch 选择 **main**、Folder 选择 **/(root)**，保存后等待部署。

## 功能

- BTCUSDT 币安公开现货价格与 5 分钟 K 线
- A 独立随机、B 低波动过滤随机、C 连续三根同向反转
- 300/600/900 根 K 线回测与 Wilson 95% 胜率区间
- 本机 localStorage 模拟信号记录、模拟结算、CSV 导出

## 重要限制

仅使用现货 K 线模拟方向，**未接入币安预测市场的实时赔率、成交价格或官方结算**。历史回测的价格参数为假设值，不能用于推断实际收益。网站不包含自动下单功能、不索取 API Key。Safari 清理网站数据会删除本机记录，请导出备份。币安 API 可能受地区网络或浏览器跨域策略影响。

## 90天历史分析

打开 https://xwflipped.github.io/Lucas-5M/backtest90.html ，选择90天、70/30样本拆分，设置假设买入价格和费用，点击“获取并回测”。会分页获取币安 BTCUSDT 5分钟公开K线，显示数据质量、训练/测试结果、日期/UTC小时拆分、Wilson 95%区间、最大回撤与盈亏平衡门槛，并支持逐笔CSV导出。

**注意**：受网络、地区限制、币安接口可用性及设备性能影响，90天请求可能失败或耗时较久。此功能是现货K线模拟，不是预测市场真实收益。策略在历史上挑选过，时间切分不等于严格的未来前瞻验证。
