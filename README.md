# ระบบประกาศข่าวสาขาหรือกลุ่ม

### ความต้องการของระบบ
- PHP 5 (5.4 - 5.6)
- PHP 5 PDO Support
- PHP GD

### การเชื่อมต่อ Database และการติดตั้ง
 - ให้เข้าไปแก้ไขไฟล์
```
app/config/db.php
---------------------- ค้นหา ---------------------------
return [
	'driver'		=> 'pdo',
	'hostname'	    => '<Your host>',
	'dbname'		=> '<Your DB name>',
	'username'	    => '<Your username>',
	'password'	    => '<Your Password>',
	'prefix'		=> 'bl_',
	'charset'		=> 'utf8'
];
```
 - ตั้งค่ารหัสผ่าน admin
```
app/controller/MigrateController.php
---------------------- ค้นหา ---------------------------
public function admin()
{
	$this->db->insert('user',[
		'email' => '<Your email>',
		'username' => '<Your username>',
		'password' => password_hash(hash('sha256','<Your password>'), PASSWORD_BCRYPT),
		'active'	=> 1,
		'created_at' => date('Y-m-d H:i:s')
	]);
	$this->db->insert('user_detail',[
		'user_id' => 1,
		'role_id' => 0,
		'firstname' => '<Your firstname>',
		'lastname' => '<Your lastname>',
		'nickname'	=> '<Your nickname>',
		'major' => 1
	]);
}
```
- ตั้งค่า app
```
app/config/app.php
---------------------- ค้นหา ---------------------------
return [
	// ex. http://172.17.42.1/ or http://domain.com/
	'url'			=> '<Your-url>',
	// ถ้าอยู่ใน subfoler
	'sub_folder'	=> '',
	// ชื่อไฟล์หน้าแรกเช่น index.php ถ้าใช้งาน htaccess ไม่ต้องกรอก
	'index'			=> '',
	// Controller แรกที่จะทำงานหน้าแรกนั่นเองครับ
	'primary'		=> 'home',
	'template'		=> 'default',
	// Session
	'session_name'	=> '<Session name>',
	'session_path'	=> '/app/session'
];
```
- สร้าง ฐานข้อมูลให้เรียบร้อย
- จากนั้น เปิดหน้าเว็บ `http://<Your domain or IP>/migrate`
