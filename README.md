# UniversityAcademicWarningSystem
高校学业预警系统 ASP.NET 课程设计

如何运行？
1. 使用 visual studio 2019或以上版本IDE打开"高校学业预警系统"目录下的"GuoxuanWebApi.sln"

2. 使用 Microsoft SQL Server 2019 + Microsoft SQL Server Management Studio 18 配置数据库

2.1. 首先打开Microsoft SQL Server Management Studio 18，并通过SQL Server 身份验证的方式使用sa账号连接到 Microsoft SQL Server 2019的服务器

2.2. (如果忘记sa密码则执行2.2.)首先通过Windows 身份验证进行连接，然后点击工具栏上的"新建查询(Ctrl+N)",键入命令"sp_password Null,'123','sa';"并执行，此时sa账户的密码被设置为123。之后右击数据库选择"断开连接"，然后重新执行2.1.

2.3. (如果使用sa密码无法登陆数据库则参考2.3.)这很可能是因为没有开启sa账户，首先通过Windows 身份验证进行连接，依次展开目录"安全性\登陆名"，此时可以看到"登陆名"目录的最下面有一个"sa"，双击它，选择"状态"页，将登录名设置为"启用(E)"，点击确定。之后右键服务名，打开"属性"，选中"安全性"页面，选中将"服务器身份验证"下的"SQL Server和Windows身份验证模式(S)"，然后重新执行2.1.

2.4. 右键点击"数据库"目录，选择"附加(A)"，在"常规"页面的"要附加的数据库(D)"下点击"添加(A)"按钮，找到并选择"C3115.mdf"，然后单击"确定"，完成对数据库的配置

2.5. (如果2.4.步骤出错则执行2.5.)点击工具栏上的"新建查询(Ctrl+N)",键入命令"sp_attach_db 'test','[...]\C3115.mdf','[...]\C3115_log.ldf';"并执行，注意这里的[...]\C3115.mdf和[...]\C3115_log.ldf指的是C3115.mdf和C3115_log.ldf的绝对路径，在文件资源管理器中查看这两个文件的属性就可以知道。

3. 在visual studio 2019或以上版本IDE中运行asp.net项目(通过IIS Express)

3.1. (如果运行过程中出现错误，可以参考3.1.1.~3.1.3.，建议执行完某一个步骤后都要重新运行项目)

3.1.1. 保证程序运行期间只有附加了C3115数据库的SQL Server服务在运行(在2.1.连接数据库的时候可以看到是哪个服务)，可以在"SQL Server 2019配置管理器"的"SQL Server服务"中查看，多余的服务停止掉。

3.1.2. 请保证附加了C3115数据库的SQL Server服务启用了TCP/IP协议，可以在"SQL Server 2019配置管理器"的"SQL Server网络配置"中，选中服务查看"TCP/IP"协议，如果显示"已禁止"，就右键启用它。

3.1.3. 如果提示某个用户无法连接到数据库，可以登录Microsoft SQL Server Management Studio 18并依次展开目录"安全性\登陆名"，找到无法登录的用户名，双击打开属性框，选中"用户映射"页，在"映射到此登录名的用户(D)"中勾选"C3115"，然后在"数据库角色成员身份(E):C3115"中勾选"db_owner"，点击确定。
