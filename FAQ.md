# 常见问题FAQ
## 无法在线搜索
duckduckgo需要有连接外网的能力，否则无法使用，会报错

## 知识库不能用
config.json里边要设置local_embedding:true，但是如果没有GPU会特别特别慢

## auto_gptq安装失败
pip install auto_gptq==0.2.0

pytorch - 尽管安装了火炬，安装auto-gptq仍无法工作（错误火炬未安装，请先安装火炬！） - Thinbug --- pytorch - install auto-gptq not working despite torch installed (error torch is not installed, please install torch first!) - Stack Overflow
https://stackoverflow.com/questions/76793175/install-auto-gptq-not-working-despite-torch-installed-error-torch-is-not-instal

Torch 未安装 · 问题 #229 · AutoGPTQ/AutoGPTQ --- Torch is not installed · Issue #229 · AutoGPTQ/AutoGPTQ
https://github.com/AutoGPTQ/AutoGPTQ/issues/229

## HooChat后台初始化参数配置
参考config_example.json创建config.json只能保留需要配置的项，其他空项要删除