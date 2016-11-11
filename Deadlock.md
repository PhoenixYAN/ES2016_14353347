#Lab4 Deaklock 死锁实验
---
##1、实验流程
###（1）编写方法类A和B
`class A`

	synchronized void methodA(B b) {
		b.last();
	}
	synchronized void last() {
		System.out.println("Inside A.last()");
	}
`class B`

	synchronized void methodB(A a) {
		a.last();
	}
	synchronized void last() {
		System.out.println("Inside B.last()");
	}
###（2）编写死锁类Deadlock  
`

	class Deadlock implements Runnable{
	A a = new A();
	B b = new B();
	Deadlock(){
		Thread t = new Thread(this);
		long count = 200000;
		t.start();
		while(count-->0);
		a.methodA(b);
	}
	public void run(){
		b.methodB(a);
	}
	public static void main(String args[]){
		new Deadlock();
	}
	}
`
### （3）编写批处理文件（Windows环境下）
`	

	cd /d %~dp0
	@echo off
	:start
	set /a var+=1
	echo %var%
	java Deadlock
	if %var% leq 1000 GOTO start
	pause

`
##2、实验结果
![jjj](http://i.imgur.com/fYYrLka.png)
##3、实验原理
###（1）死锁的四个必要条件
互斥条件：一个资源每次只能被一个进程使用
请求与保持条件：一个进程因请求资源而阻塞时，对已获得的资源保持不放
不剥夺条件:进程已获得的资源，在末使用完之前，不能强行剥夺
循环等待条件:若干进程之间形成一种头尾相接的循环等待资源关系
###（2）程序产生死锁的原因
由于synchronized修饰的代码块一次性只能访问一次，当执行b.methodB(a)时，若上一个进程的a.methodA(b)还没有执行完毕，a.last不能执行。而又因为此当前线程的b执行者methodB函数，a.last不能执行，因此上一个进程的a.methodA(b)也无法继续执行，因此产生了死锁。
