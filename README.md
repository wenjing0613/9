package week7;
import java.util.Date;
import java.util.Scanner;
 
import com.ww.entity.LogInfo;
import com.ww.entity.UserAcount;
 
public class UserAcountService {
	UserAcount ua;
	Scanner inputScanner=new Scanner(System.in);
	//声明一个日志数组，用于保存用户的操作数据
	LogInfo[] ls=new LogInfo[10];
	
	
	//登录的方法
	public void login(){
		initUser();//调用方法
		boolean f;
		int count=0;//登录的次数
		do {
			System.out.println("请输入账号：");
			String name=inputScanner.next();
			System.out.println("请输入密码：");
			String pwd=inputScanner.next();
			f=ua.login(name, pwd);
			count++;
			if (!f) {
				System.out.println("登录失败，您还有"+(3-count)+"次机会！");
			}
		} while (f==false&&count<3);
		//1、登录成功
		//2、失败次数达到3次
		if (f) {
			//显示功能菜单
			int choose;
			do {
				choose=showMenu();
				switch (choose) {
				case 1://存款
					addMoney();
					break;
				case 2://取款
					getMoney();
					break;
				case 3://查询
					showLogInfo();
					break;
 
				default://退出
					System.exit(0);
					System.out.println("谢谢使用，已退出！");
					break;
