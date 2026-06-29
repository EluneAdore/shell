
1.一键升级（并剔除无用的包）
```
apt update -y && apt full-upgrade -y
```
2.ZEN内核 Debian / Ubuntu / Arch：默认启用bbr+fq，需要关闭ECN
```
https://liquorix.net/
```
3.ZEN内核官方一键安装脚本
```
curl -s 'https://liquorix.net/install-liquorix.sh' | bash
```
4.关闭ECN：先清除所有ECN相关的旧配置，然后将 net.ipv4.tcp_ecn 的值写入专用的高优先级配置文件 /etc/sysctl.d/99-sysctl.conf 中，最后刷新系统配置
```
sed -i '/net.ipv4.tcp_ecn/d' /etc/sysctl.d/99-sysctl.conf /etc/sysctl.conf 2>/dev/null; echo "net.ipv4.tcp_ecn=0" >> /etc/sysctl.d/99-sysctl.conf; sysctl --system >/dev/null 2>&1
```

5.查看当前运行的算法+查看当前队列算法+查看ECN的开启状态+查看系统内核版本号及系统名称
```
echo -e "当前算法: [\e[38;2;0;255;0;1m$(cat /proc/sys/net/ipv4/tcp_congestion_control)\e[0m]\n队列算法: [\e[38;2;0;255;0;1m$(sysctl -n net.core.default_qdisc)\e[0m]\nECN状态:  $([ "$(sysctl -n net.ipv4.tcp_ecn)" -eq 0 ] && echo -e "\e[38;2;0;255;0;1m[关闭]\e[0m" || echo -e "\e[38;2;0;255;0;1m[开启]\e[0m")\n系统内核: [\e[38;2;0;255;0;1m$(uname -sr)\e[0m]"
```
