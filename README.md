# think-filesystem-driver-github
ThinkPHP 的github 文件系统驱动，可以将一个仓库作为文件库


## 安装

~~~ shell
composer require yangweijie/think-filesystem-driver-github
~~~

## 使用

配置
token 需 开发着自己去 github 里 配置 
~~~ php
'github'=>[
    'type'=>'github',
    'branch'=>'main', // main 可以不配，master 等可以配置一下
    'token'=>Env::get('filesystem.GITHUB_ACCESS_TOKEN', ''),
    'username'=>'username',
    'repository'=>'repository',
    'hostIndex'  => 'jsdelivr', // 目前支持 github 、 jsdelivr 、 fastgit 
],
~~~

### 本地文件上传

~~~
$file = public_path().'favicon.ico';
$githubDisk = Filesystem::disk('github');
if(!$githubDisk->has('favicon.ico')){
    $ret = $githubDisk->put('favicon.ico', file_get_contents($file));
}
$url = $githubDisk->url('favicon.ico');
// https://cdn.jsdelivr.net/gh/username/repository@main/favicon.ico
~~~

### 表单上传

~~~
// 获取表单上传文件 例如上传了001.jpg
$file = request()->file('image');
// 上传到本地服务器
$savename = \think\facade\Filesystem::disk('github')->putFile( 'topic', $file);
~~~

