
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
4.关闭ECN
```
echo "net.ipv4.tcp_ecn=0" >> /etc/sysctl.conf && sysctl -p
```

5.查看当前运行的算法+查看当前队列算法+查看ECN的开启状态+查看系统内核版本号及系统名称
```
echo -e "当前算法: [\e[38;2;0;255;0;1m$(cat /proc/sys/net/ipv4/tcp_congestion_control)\e[0m]\n队列算法: [\e[38;2;0;255;0;1m$(sysctl -n net.core.default_qdisc)\e[0m]\nECN状态:  $([ "$(sysctl -n net.ipv4.tcp_ecn)" -eq 0 ] && echo -e "\e[38;2;0;255;0;1m[关闭]\e[0m" || echo -e "\e[38;2;0;255;0;1m[开启]\e[0m")\n系统内核: [\e[38;2;0;255;0;1m$(uname -sr)\e[0m]"
```
