```
-- 目录操作，文件操作




# 目录

-- 目录结构

/bin：基本用户命令，所有用户都能用（单用户模式也可用）
/sbin：系统管理命令，通常需要 root 权限
/usr/bin：大部分用户命令（系统启动后挂载）

-- /etc配置
/etc/hostname    # 主机名
/etc/hosts       # DNS 解析
/etc/nginx/      # Nginx 配置
/etc/ssh/        # SSH 配置

-- /var日志
/var/log/        # 系统日志（最重要）
/var/log/syslog  # 系统日志
/var/log/nginx/  # Web 服务器日志
/var/cache/      # 缓存数据
/var/tmp/        # 持久临时文件（重启不清空）
/var/spool/      # 打印队列、邮件队列

-- /usr用户
/usr/bin/        # 大部分用户命令
/usr/sbin/       # 额外的系统命令
/usr/lib/        # 库文件
/usr/local/      # 本地安装的软件（源码编译默认位置）
/usr/share/      # 共享数据（文档、图标、字体）
/usr/include/    # C/C++ 头文件

-- /proc进程
/proc/cpuinfo    # CPU 信息
/proc/meminfo    # 内存信息
/proc/version    # 内核版本
/proc/uptime     # 系统运行时间
/proc/[PID]/     # 每个进程的信息目录

-- /dev设备
/dev/sda         # 第一块 SATA/SCSI 硬盘
/dev/sda1        # 第一块硬盘的第一个分区
/dev/nvme0n1     # NVMe 固态硬盘
/dev/tty         # 当前终端
/dev/random      # 随机数生成器
/dev/null        # 黑洞（丢弃所有写入）

-- 目录操作

-- 切换目录
pwd                 # 显示当前所在目录的绝对路径
cd /home/user       # 切换到指定目录
cd ..(/..)          # 切换到上一/两级目录
cd ~(username)      # 切换到用户的家目录
cd -                # 返回到上一次所在的目录
cd /                # 切换到根目录

-- 列出目录内容
ls -i/-Z            # 列出当前目录内容(显示 inode 号/SELinux 上下文)
ls -l/-a/-la/-lh    # 显示详细信息/所有文件/可读格式
ls -lt/ltr/lS       # 按新/旧修改时间/文件大小排序
ls -R               # 递归显示子目录
ls -d */            # 只显示目录
ls *.txt            # 列出所有txt文件
ls file?            # 匹配file后跟一个字符
ls [abc]*           # 以a、b或c开头的文件

-- 增删目录
mkdir dirname1,dirname2         # 创建目录
mkdir -p parent/child/grandchild # 递归创建（父目录不存在时自动创建）
mkdir -m 755 dirname            # 创建时指定权限
mkdir -v dirname                # 显示创建信息
rmdir dir1 dir2                 # 删除多个空目录
rmdir -p parent/child           # 递归删除空目录（父目录也空才删）
rmdir -v dirname                # 显示删除信息


# 文件操作

-- 创建删除文件
touch file1.txt file2.txt       # 创建空文件（已存在则更新修改时间）
touch -t 202312311200 file      # 设置指定时间戳
touch -r source.txt target.txt  # 复制时间戳
touch -d "2023-12-31" file      # 设置日期
rm file1.txt file2.txt          # 删除多个文件
rm -i file.txt                  # 删除前确认
rm -f file.txt                  # 强制删除（不提示，忽略不存在的文件）
rm -r dir/                      # 递归删除目录及其内容
rm -rf dir/                     # 强制递归删除（危险！谨慎使用）
rm -v file.txt                  # 显示删除信息
rm *.log                        # 删除所有log文件

-- 复制文件
cp source.txt dest.txt          # 复制文件
cp file1.txt file2.txt dir/     # 复制多个文件到目录
cp -i source.txt dest.txt       # 覆盖前提示确认
cp -r source_dir/ dest_dir/     # 递归复制目录
cp -a source_dir/ dest_dir/     # 保留属性（权限、时间等）
cp -u source.txt dest.txt       # 只在源文件更新时复制
cp -v source.txt dest.txt       # 显示复制过程
cp -p source.txt dest.txt       # 保留文件属性
cp -l source.txt dest.txt       # 创建硬链接而不是复制
cp -s source.txt dest.txt       # 创建符号链接

--移动重命名文件
mv old.txt new.txt                # 重命名
mv file.txt /path/to/dir/         # 移动文件
mv dir1/ dir2/                    # 移动目录
mv -i source.txt dest.txt         # 覆盖前提示
mv -u source.txt dest.txt         # 只在源文件更新时移动
mv -v file.txt /path/to/          # 显示移动过程
mv -n source.txt dest.txt         # 不覆盖已存在的文件
rename 's/旧字符串/新字符串/' 文件   # 批量重命名
rename 's/\.txt$/\.bak/' *.txt    # 将.txt改为.bak
rename 's/^/prefix_/' *           # 添加前缀
rename 's/\.jpeg$/\.jpg/' *.jpeg  # 更改扩展名

-- 查看文件

cat (-n/-b/-A) file.txt     # 显示文件内容(显示行号/非空行行号所有字符)
tac                           反向显示（最后一行在前）
less (-N/-S) file.txt       # 分页查看 (显示行号/不换行)
空格:下一页   b:上一页   Enter:下一行   k:上一行   g:第一行   G:最后一行   /pattern:向下搜索   ?pattern:向上搜索   n:下一个匹配    N:上一个匹配    q:退出
head -n 20 file.txt         # 显示前20行
tail -n 20 file.txt         # 显示最后20行

-- 文件属性

file file.txt              # 显示文件类型
file /bin/ls               # 查看命令文件类型
stat file.txt              # 显示文件详细属性
du                         # 显示当前目录下所有目录大小

-- 文件查找

find /home -name "*.txt"          # 按名称查找:查找txt文件
find / -iname "README"                       忽略大小写
find . -name "file?"                         通配符查找
find / -type f/d/l                # 按类型查找:查找普通文件/目录/符号链接
find / -size +100M/-1k/10M        # 按大小查找:大于100M/小于1k/精确10M
find / -mtime -7/+30              # 按时间查找:7天内修改的文件/30天前修改
find / -atime -1                             1天内访问
find / -perm 755/-644             # 按权限查找:精确权限/至少包含
find / -user root                 # 属于root用户
find / -group root                # 属于root组
find . -empty                     # 查找空文件
which 命令                         # 查找命令位置
locate (-i/-n 10)filename         # 查找数据库文件（sudo updatedb 更新数据库）

-- 解压打包

tar -czvf archive.tar.gz file1 dir1/          # 创建tar.gz
tar -czvf archive.tar.gz --exclude="*.log" .  # 排除文件
tar -xzvf archive.tar.gz [-C /target/path]    # 解压到指定目录
tar -tzvf archive.tar.gz                      # 列出内容

-- 常用

查找大文件
find / -type f -size +100M -exec ls -lh {} \;
批量修改扩展名
for f in *.jpeg; do mv "$f" "${f%.jpeg}.jpg"; done
统计目录下代码行数
find . -name "*.py" -exec cat {} \; | wc -l
查找并删除7天前的日志
find /var/log -name "*.log" -mtime +7 -delete
查看占用空间最大的目录
du -h /home | sort -rh | head -10
查找重复文件
find . -type f -exec md5sum {} \; | sort | uniq -w32 -dD


# 文件内容处理

-- grep

grep [-?] "pattern" file.txt        # 搜索文件
-i  忽略大小写
-n  显示行号
-v  反向匹配（不包含）
-c  统计匹配行数
-l  只显示文件名
grep -E "pattern1|pattern2" file    # 扩展正则
grep -A/B/C 5 "error" log.txt       # 显示匹配行及后/前/前后5行
grep -r "pattern" /path/            # 递归搜索目录

-- sort

sort [-?] file.txt                   # 默认排序
-r    反向排序
-n    按数字排序
-h    人类可读数字（1K,2M）
-u    去重排序
-t:   指定分隔符

-- tr

tr 'a-z' 'A-Z' < file.txt       # 小写转大写
tr -d ' '      < file.txt       # 删除空格
tr -s ' '      < file.txt       # 压缩多个空格
tr ',' '\t'    < file.txt       # 逗号转制表符

-- wc

wc -l data.csv            # 统计行数
wc -w README.md           # 统计单词数
wc -c file.txt            # 统计字符数
wc file1.txt  file2.txt   # 统计全部

-- sed（查找替换、插入删除行）

命令          含义           示例
s/old/new/  替换           sed 's/,/|/'
d           删除行          sed '/error/d'
p           显示行（配合-n）sed  -n '5p'
i           行前插入         sed '2i\new line'
a           行后追加         sed '2a\new line'
sed 's/old/new/'          file.txt  # 基础替换（只改每行第一个匹配）
sed 's/old/new/g'         file.txt  # 全局替换（一行内所有匹配）
sed -i 's/old/new/g'      file.txt  # 保存回文件（-i 直接修改原文件，建议先不加预览）
sed 's#/usr/local#/opt#g' file.txt  # 使用其他分隔符（处理路径时好用）

-- awk（按列处理、数据汇总、生成报告）

变量        含义           示例
NR        当前行号     awk '{print NR, $0}'
NF        当前行字段数   awk '{print NF}'
$0        整行内容     awk '{print $0}'
$1...$n   第n个字段        awk '{print $1, $NF}'
OFS       输出字段分隔符  awk -F',' '{print $1,$2}' OFS='|'
FS        输入字段分隔符  awk -F':' 或 awk 'BEGIN{FS=":"}'
RS        输入行分隔符   awk 'BEGIN{RS=";"}'
awk '{print $1, $3}' file.txt          # 打印第1列和第3列（默认空格/TAB分隔）
awk -F',' '{print $1, $2}' data.csv    # 指定分隔符为逗号（CSV文件）
awk '{print $NF}' file.txt             # 打印最后一列
awk '{print NR, $0}' file.txt          # 打印行号
awk -F',' '$3 > 100' data.csv          # 第3列 > 100 的行
awk -F',' '$2 == "ERROR"' log.csv      # 第2列等于 "ERROR" 的行
awk -F',' '$5 ~ /^2023-01/ ' data.csv  # 第5列匹配正则
awk -F',' '{sum += $3} END {print "Total:", sum}' data.csv       # 计算第3列总和
awk -F',' 'max < $3 {max = $3} END {print "Max:", max}' data.csv # 求最大值
awk 'NR==FNR{a[$1];next} $1 in a' file1.txt file2.txt            # 比较两个文件的第1列

-- 模版
替换并删除空行
sed 's/old/new/g' file | sed '/^$/d'
过滤+统计
awk -F',' '$3 > 100 {sum+=$4; count++} END {print sum/count}'
分组汇总
awk -F',' '{count[$2]++; sum[$2]+=$3} END {for(k in count) print k, count[k], sum[k]}'
```