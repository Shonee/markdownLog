

###### 2020-03-17: 判断指定路径文件（夹）是否存在

```c#
//在上传文件时经常要判断文件夹是否存在，如果存在就上传文件，否则新建文件夹再上传文件
if (System.IO.Directory.Exists(path))//如果不存在就创建file文件夹
{
　　System.IO.Directory.CreateDirectory(path);
}
System.IO.Directory.Delete(path,true);//删除文件夹以及文件夹中的子目录，文件   
 
//判断文件的存在
if (System.IO.File.Exist(filePath))
{
	//存在文件
} 
else
{
   Directory.CreateDirectory(Path);//创建指定的文件目录
   File.Create(filePath);////创建文件
}

```

###### 2020-03-23 比较两个文件是否相同（使用hash码比较方法）

```c#
var hash = System.Security.Cryptography.HashAlgorithm.Create();
var remoteFileHash = hash.ComputeHash(FileUtil.BytesToStream(info.FileData));
var localFileHash = hash.ComputeHash(FileUtil.FileToStream(filePath));
if (BitConverter.ToString(remoteFileHash) == BitConverter.ToString(localFileHash)) 
{
   MessageUtil.ShowTips("文件相同");
}

//比较两个图片文件是否一样，转换成base64比较
string localImage = Convert.ToBase64String(FileUtil.FileToBytes(this.pictureBox1.ImageLocation));
int localSize = FileUtil.GetFileSize(this.pictureBox1.ImageLocation);
string remoteImage = Convert.ToBase64String(imageInfo.FileData);
FileUtil.CreateFile(serverRealPath, imageInfo.FileData);
int remoteSize = FileUtil.GetFileSize(serverRealPath);

if (!remoteImage.Equals(localImage))
{
    FileUtil.DeleteFile(this.pictureBox1.ImageLocation);
    FileUtil.CreateFile(serverRealPath, imageInfo.FileData);
}
```

###### 2020-03-23 文件 二进制文件和文件流的相互转换

```c#
//流文件转换成二进制
Stream stream = File.Open(filePath, FileMode.Open);
byte[] bytes = new byte[stream.Length];
stream.Read(bytes, 0, bytes.Length);//从头至尾将流读取到二进制文件中
stream.Seek(0, SeekOrigin.Begin);//读取完毕后，将流的位置设置为开始

//二进制转换成流
Stream newDtream = new MemoryStream(bytes);
```

