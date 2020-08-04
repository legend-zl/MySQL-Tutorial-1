在本教程中，您将学习如何使用MySQL `IF`语句来根据条件执行一个SQL代码块。

MySQL `IF`语句允许您根据表达式的某个条件或值结果来执行一组SQL语句。 要在MySQL中形成一个表达式，可以结合文字，[变量](http://www.yiibai.com/mysql/variables-in-stored-procedures.html)，运算符，甚至函数来组合。表达式可以返回`TRUE`,`FALSE`或`NULL`，这三个值之一。

> 请注意，有一个[IF函数](http://www.yiibai.com/mysql/if-function.html)与本教程中指定的`IF`语句是不同的。

## MySQL IF语句语法

下面说明了`IF`语句的语法：

```sql
IF expression THEN 
   statements;
END IF;
```

如果表达式(`expression`)计算结果为`TRUE`，那么将执行`statements`语句，否则控制流将传递到`END IF`之后的下一个语句。

以下流程图演示了`IF`语句的执行过程：

![img](../images/631190840_68526.jpg)

### MySQL IF ELSE语句

如果表达式计算结果为`FALSE`时执行语句，请使用`IF ELSE`语句，如下所示：

```sql
IF expression THEN
   statements;
ELSE
   else-statements;
END IF;
```

以下流程图说明了`IF ELSE`语句的执行过程：

![img](../images/378190849_92477.jpg)

## MySQL IF ELSEIF ELSE语句

如果要基于多个表达式有条件地执行语句，则使用`IF ELSEIF ELSE`语句如下：

```sql
IF expression THEN
   statements;
ELSEIF elseif-expression THEN
   elseif-statements;
...
ELSE
   else-statements;
END IF;
```

如果表达式(`expression`)求值为`TRUE`，则`IF`分支中的语句(`statements`)将执行；如果表达式求值为`FALSE`，则如果`elseif_expression`的计算结果为`TRUE`，MySQL将执行`elseif-expression`，否则执行`ELSE`分支中的`else-statements`语句。具体流程如下 -

![img](../images/233080853_60470.jpg)

## MySQL IF语句示例

以下示例说明如何使用`IF ESLEIF ELSE`语句，`GetCustomerLevel()`存储过程接受客户编号和客户级别的两个参数。

*首先*，它从`customers`表中获得信用额度

然后，根据信用额度，它决定客户级别：`PLATINUM` , `GOLD` 和 `SILVER` 。

参数`p_customerlevel`存储客户的级别，并由调用程序使用。

```sql
USE yiibaidb;

DELIMITER $$

CREATE PROCEDURE GetCustomerLevel(
    in  p_customerNumber int(11), 
    out p_customerLevel  varchar(10))
BEGIN
    DECLARE creditlim double;

    SELECT creditlimit INTO creditlim
    FROM customers
    WHERE customerNumber = p_customerNumber;

    IF creditlim > 50000 THEN
 SET p_customerLevel = 'PLATINUM';
    ELSEIF (creditlim <= 50000 AND creditlim >= 10000) THEN
        SET p_customerLevel = 'GOLD';
    ELSEIF creditlim < 10000 THEN
        SET p_customerLevel = 'SILVER';
    END IF;

END$$
```

以下流程图演示了确定客户级别的逻辑 -

![img](../images/244080857_22798.png)

在本教程中，您已经学会了如何使用MySQL `IF`语句根据条件执行一个SQL代码块。