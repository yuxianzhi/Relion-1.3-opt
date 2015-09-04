# Relion-1.3-opt
冷冻电镜图像三维重建程序Relion-1.3的优化（包含通信框架优化和分发任务优化）和容错（一个节点失效）研究，
实现了树状集合通信框架，多节点分发任务，一个节点失效时MPI可以继续运行，使用socket代替MPI做通信。
包含以下文件：
1）relion-1.3.tar.bz2
  原来的relion-1.3版本的代码
2）relion-1.3-opt1.rar文件
  加了通信框架优化
3）relion-1.3-opt2.rar文件
  加了通信框架优化和分发任务框架（两个分发任务的节点）的优化
4）relion-1.3-down.rar文件
	relion的利用MPI（Intel或者MPICH，保证一个进程失效不会自动清理其它进程）容错实现版本，假设计算节点估计自己将要关机时，主动发送
	一个消息给master（0号进程），0号进程告知其余进程停下来，先将失效进程移除通信域，这样失效进程就不会对其余进程产生影响，
	之后再进行后续计算工作。
5）relion-1.3-socket.rar文件
  relion的socket实现版本，加上了epoll的IO多路复用技术。虽然没有调用MPI的函数，但是使用mpicc来编译的，真正调用的是socket实现的函数，使用MPI.c启动多进程
	MPI.c是类似于mpirun的启动程序，需要单独编译gcc -std=c99 -o main MPI.c。
	其余的和relion一模一样，运行不是使用mpirun，而是MPI.c编译出的main可执行程序
