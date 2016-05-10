# remoteMysql
������Ѷ��ƽ̨�Ľ�����nodejs���������Ѷ��mysql��mongoose���ݿ�

1�������ǵ�½��Ѷ�ƣ�����https://passport.qcloud.com/����½֮�������ȡ�����������ͼ
 

2�������Ʋ�Ʒ->���ݿ�->CDB for MYSQL->����ѡ����ѡ�������Ŀ�������ֿ�ʹ��һ���£��������
3����ҳ->���Ͻǲ�Ʒ����->ʹ���е����ݿ�,��ʱ���ǻῴ��һ��ʵ�����������ǽ������ҳ���ʵ������һЩ����������
ʵ��������������ģ�������ַ���뿪�����������ǾͲ������Լ�����Ŀ�кͱ��ط��������ݿ⡣�����˺Ź���ҳ���޸��Լ���root���룬Ȼ�������Ͻǵĵ�¼���ݿ�
 
4.��½���֮������ͼ
����ͱ��ؿͻ��˲���������ͬ���ҾͲ���ϸ������
 

����ʹ��һ��demo��˵����β�����mysql���ݿ�
1����ʵ�������½�һ��Ϊnodejs�����ݿ⣬Ȼ���½�һ��Ϊemployee�ı��½��ĸ��ֶ� name  sex   age   email��������Ϊint������ȫ��Ϊvarchar��ʽ 
2���½�һ��TimLiu���ļ���,��cmd��cd TimLiu, ��ʼ����Ŀnpm init ,����������ʾһ��һ���Ĳ������ɣ���װmysqlģ�飬npm insitall mysql, ���ģ���������Ҫ������mysql���ݿ⡣
3���½�һ��model.js �ļ���
var mysql = require(��mysql��);
var connection = mysql.createConnection({
    host:'',
    user:'root',
    password:'123abc',
    database:' nodej,
    port:6445
})
connection.connect();
�����hostΪ��������Ѷ���Ͽ�ͨ�����ַ���˿ں�Ҳ����������ַ���棬ע��Ҫ��������ַд�ֿ����û�ΪĬ�ϵĹ���Ա�û�������Ϊ��������ƽ̨�����õ����룬���ݿ�Ϊ���Ǵ�����nodejs���ݿ⡣
���������Ƕ����ݿ������ɾ�Ĳ����

function addEmployee(){
    var employeeInsertSql = 'INSERT INTO employee(name,sex,age,email) VALUES(?,?,?,?)';
    var employeeInsertSql_Params = ['Tim','��',22,'18818216454@163.com']
    connection.query(employeeInsertSql,employeeInsertSql_Params,function(err,result){
        if(err) console.log('[INSERT ERR]-',err.message);
        console.log(result);
    }) 
}

addEmployee()


/**
 * ����Ա��
 */

function insertEmployee(){
    var employeeUpdateSql = "UPDATE employee SET name = ? WHERE age =?";
    var employeeUpdateSql_Params = ['Peter',22];
    connection.query(employeeUpdateSql,employeeUpdateSql_Params,function(err,result){
        if(err) console.log('[UPDATE ERR]-',err.message);
        console.log(result);
    })
}

 insertEmployee();

/**
 * ��ѯԱ��
 * 
 */

function getEmployee(){
    var employeeGetSql = "SELECT * FROM employee";
    connection.query(employeeGetSql,function(err,result){
        if(err) console.log('[SELECT ERR]-',err.message);
        console.log(result);
    })
}


getEmployee();

/**
 * ɾ��Ա��
 */

function deleteEmployee(){
    var employeeDeleteSql = "DELETE employee WHERE name = ?";
    var employeeDeleteSql_Params = 'Peter';
    connection.query(employeeDeleteSql,employeeDeleteSql_Params,function(err,result){
        if(err) console.log('[DELETE ERR]-',err.message);
        console.log(result);
    })
    
}

deleteEmployee();


�������ǾͿ������Ĳ������ݿ���

�����������Ŀ��ģ�黯����������model�����½�һ��employee_two.js,��������
var mysql = require('mysql');

var connection = mysql.createConnection({
    host:'',
    user:'root',
    password:'',
    database:'nodejs',
    port:
})
connection.connect();


/**
 * ����Ա��
 * @param {String} employee
 * @param {Function} callback
 */

exports.addEmployee=function(employee,callback){
    var employeeInsertSql = 'INSERT INTO employee(name,sex,age,email) VALUES(?,?,?,?)';
    var employeeInsertSql_Params = [employee.name,employee.sex,employee.age,employee.email]
    connection.query(employeeInsertSql,employeeInsertSql_Params,callback)
}


/**
 * ����Ա��
 * @param {String} employee
 * @param {Function} callback
 */

exports.updateEmployee = function(name,age){
    var employeeUpdateSql = "UPDATE employee SET name = ? WHERE age =?";
    var employeeUpdateSql_Params = ['Peter',22];
    connection.query(employeeUpdateSql,employeeUpdateSql_Params,function(err,result){
        if(err) console.log('[UPDATE ERR]-',err.message);
        console.log(result);
    })
}

/**
 * ��ѯԱ��
 * 
 */

exports.getEmployee = function(){
    var employeeGetSql = "SELECT * FROM employee";
    connection.query(employeeGetSql,callback)
}

/**
 * ɾ��Ա��
 * @param {String} name
 */

exports.deleteEmployee = function(name){
    var employeeDeleteSql = "DELETE employee WHERE name = ?";
    var employeeDeleteSql_Params = 'Peter';
    connection.query(employeeDeleteSql,employeeDeleteSql_Params,callback)
    
}


���ڸ�Ŀ¼���½�index.js,��������
var db = require('./model/employee_two');


//����Ա��
var employee = {
    name:'lisa',
    age:22,
    sex:"Ů",
    email:'99533212@qq.com'
}
db.addEmployee(employee,function(err,result){
    if(err) console.log("[INSERT err]-",err.message)
    console.log(result);
})

//ɾ��Ա��
db.deleteEmployee('Peter',function(err,result){
    if(err) console.log("[DELETE err]-",err.message)
    console.log(result);
})

//����Ա��
db.updateEmployee('Tim',23,function(err,result){
    if(err) console.log("[UPDATE err]-",err.message)
    console.log(result);
})

//��ѯԱ��
db.getEmployee(function(err,result){
    if(err) console.log("[GET err]-",err.message)
    console.log(result);
})


