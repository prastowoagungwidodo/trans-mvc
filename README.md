trans-mvc
=========

Write less, FUN More

=================================

Membuat Controller 

file: home.php
<pre>
class Home_Conteroller{
  function index(){
  
  }
}
</pre>

Membuat Model
Model dibuat per table

file user.php
<pre>
class user extend Model{
  public $table = 't_user';
  public $prmary_key = 'user_id';
  public $status_field = 'user_status'; // Digunakan ketika opsi permanentDelete = false. Data tidak akan dihapus dari database hanya akan diberi value d
  public $permanentDelete = false;
  
  function relations(){
    return array(
      't_department'=>array(
          'LEFT JOIN',
          'user_dept',
          'department_id',
          true              // Convert data menjadi varchar. ini agar tidak terjadi error ketika kedua field yang di join memiliki tipe data yang berbeda
      )
    );
  }
}
</pre>
Menggunakan model pada Controller

1. Load model

<pre>
$user = load::model('user');
// Mengambil data user
$user->setLimit(10); // Set Limit
$user->setPage(2); // Set halaman 2
$user->setCondition('user_status = \'y\''); // Condition tanpa WHERE

var_dump($user->read());

// Returnnya adalah:

array(
  'total_data'=>100,
  'total_page'=>10,
  'page'=>2,
  'keyword'=>'',
  'records'=>array(......)
);

</pre>
<pre>
// Searching field
$user->setKeyword('Agung'); // Keyword
$user->setSearchIn('fullname'); // Field table
var_dump($user->read());
</pre>
<pre>
// Sort Order
$user->setOrderBy('username');
$user->setOrderTYpe('ASC'); // ASC atau DESC
</pre>
<pre>
// Insert data
$user->setData('username','BEJO');
$user->setData('user_id','123123123');
$user->insert();

atau 

$user->setDataArray($_POST);
$user->insert();
</pre>
<pre>
// Update Data

$user->setId($_POST['user_id']);
$user->setDataArray($_POST);
$user->update();
</pre>
<pre>
// Delete Data
$user->setId($_POST['user_id']);
$user->delete();

</pre>




