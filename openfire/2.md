如果发布版本时遇到

`SSL peer shut down incorrectly`

的问题，就上加

`-Dhttps.protocols=TLSv1.2`

参数再执行一次，应该就可以成功发布了

