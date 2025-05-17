# 简介

本文主要介绍如何配置树莓派的VNC系统。

## 注意事项

在树莓派4中，如果在没有连接物理显示器的情况下，使用vnc,会发现vnc的速度非常的慢，可以通过以下的方法来修改。

```sh
# 修改/boot/config.txt
# 修改成下面所示，注意需要将dtoverlay=vc4-kms-v3d注释掉，默认是enable的
#My Buster vncserver and or client was running very well.
#My Buster and Bullseye config.txt display setting are:
framebuffer_width=1024
framebuffer_height=768

hdmi_group=2
hdmi_mode=16
#dtoverlay=vc4-kms-v3d

# 配置修改完成后，重启，然后配置下面的dmt模式，配置完成之后再重启
#In Buster I also had to run raspi-config to make vncserver working with:
#Advanced Options-> Resolution->resolution->dmt mode 16 1024&768
```