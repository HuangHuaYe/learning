# SQL/NoSQL注入

注入攻击是指当所执行的一些操作中有部分由用户传入时, 用户可以将其恶意逻辑注入到操作中. 当你使用 eval, new Function 等方式执行的字符串中有用户输入的部分时, 就可能被注入攻击. XSS 就属于一种注入攻击. 如果执行的命令中有部分属于用户输入, 也可能被注入攻击.

### 注入方式:

1. 数字注入:

    在浏览器地址栏输入[`learn.me/sql/article.php?id=1`](http://learn.me/sql/article.php?id=1%EF%BC%8C%E8%BF%99%E6%98%AF%E4%B8%80%E4%B8%AAget%E5%9E%8B%E6%8E%A5%E5%8F%A3%EF%BC%8C%E5%8F%91%E9%80%81%E8%BF%99%E4%B8%AA%E8%AF%B7%E6%B1%82%E7%9B%B8%E5%BD%93%E4%BA%8E%E8%B0%83%E7%94%A8%E4%B8%80%E4%B8%AA%E6%9F%A5%E8%AF%A2%E8%AF%AD%E5%8F%A5%EF%BC%9A)

    这个一个get请求,后段相应的会执行sql语句:

        $sql = "SELECT * FROM article WHERE id =",$id

    正常情况下，应该返回一个id=1的文章信息。那么，如果在浏览器地址栏输入：[`learn.me/sql/article.php?id=](http://learn.me/sql/article.php?id=-1)-1 OR 1 =1`

    这就是一个SQL注入攻击了，可能会返回所有文章的相关信息。为什么会这样呢？

    这是因为，id = -1永远是false，1=1永远是true，所有整个where语句永远是ture，所以where条件相当于没有加where条件，那么查询的结果相当于整张表的内容

2. 字符串注入:

    假设用户输入账户和密码进行登陆,后段执行的sql可能如下:

        select * from user where username = 'user' and password = '123'

    - `user'#`

            SELECT * FROM user WHERE username = 'user'#'ADN password = '111'

    - `user'--`

            SELECT * FROM user WHERE username = 'user'-- 'AND password = '111'

    注意密码验证被注释了,这时候就不用验证密码就可以登陆.

    ### 防御手

    1）严格检查输入变量的类型和格式

    对于整数参数，加判断条件：不能为空、参数类型必须为数字

    对于字符串参数，可以使用正则表达式进行过滤：如：必须为[0-9a-zA-Z]范围内的字符串

    2）过滤和转义特殊字符

    在username这个变量前进行转义，对'、"、\等特殊字符进行转义，如：php中的addslashes()函数对username参数进行转义

    3）利用mysql的预编译机制

    把sql语句的模板（变量采用占位符进行占位）发送给mysql服务器，mysql服务器对sql语句的模板进行编译，编译之后根据语句的优化分析对相应的索引进行优化，在最终绑定参数时把相应的参数传送给mysql服务器，直接进行执行，节省了sql查询时间，以及mysql服务器的资源，达到一次编译、多次执行的目的，除此之外，还可以防止SQL注入。具体是怎样防止SQL注入的呢？实际上当将绑定的参数传到mysql服务器，mysql服务器对参数进行编译，即填充到相应的占位符的过程中，做了转义操作。