<div align="center">
The <b>English</b> version is below the <b>Chinese</b> version.
</div>

# DIRECTOR加密文件的方法之一


A在做一个项目，有很多文件，全部导入Director，工作量巨大，而且CAST会很大，所以A想用外链材料的方式，但是担心文件泄露。

最好的解决方法是什么?

答:如果谈资料加密，有很多方法，对于LINGO不是很熟练的朋友来说，最方便的是BUDAPI提供的几个加解密命令。

- baEncryptFile 文件加解密函数，本函数使用"或"运算对文件进行加密。解密的时候，用同样的密码再执行一遍本函数，这样就可以使文件恢复本来面目。

- baEncryptText加密一个字符串.

- baDecryptText函数将一个被baEncryptText函数加密的字符串解密。

# 实施过程

首先，用baEncryptFil函数对素材加密。

## 函数语法格式
注意，lingo注解是"--"，但md不支持lingo语言，这里把注解转化为js的"/\*..\*/"、"//"表达。

```js
/*
* 参数类型：
* String（字符型），String
* FileName（文件名）：指代要被加密或解密的文件名
* Key（密钥）：指代用来解密的密码字串
*/
baEncryptFile(String, FileName, Key)
```


## 示例代码：
```js
on encrypt
	// 这是即将要加密的素材存放路径
	tfolder=the moviepath&"image/" 
	// 查找符合指定格式的第一个文件，这里的以JPG为例
	tfile=  baFindFirstFile(tfolder, "*.jpg")
	
	//下面的循环体是查找所有指定格式的文件，并且加密。
	//如果找到了指定格式的文件
	repeat while tfile<>"" then
		// 加密文件，假定加密密码为123
		baEncryptFile( tfile , "123" )
		//查找下一个文件
		tfile=baFindNextFile()
	end repeat

	//提示加密完成
	alert "素材加密完成"
   end

```

注：对文件实施加密前，最好将原始文件备份。

# 加密文件的调用

被加密了的文件，Director就无法直接导入或者调用了，必须先解密后才可以使用。

```js
on DecryptFile
	// 获取系统临时文件夹
	tfile=baSysFolder("temp")
	// 加已经加密了的文件拷贝到系统临时文件夹,这里以当前运行路径下的IMAGE文件夹下的02.jpg为例
	baCopyFile( the moviepath&"image/02.jpg" ,tfile&"02.jpg" , "Always" )
	//解密文件，注意，这里是对拷贝到临时文件夹下的文件进行解密
	baEncryptFile( tfile&"02.jpg" , "123")
	// 导入文件，这里导入的也是临时文件夹下的文件
	member(100).importFileInto(tfile&"02.jpg" )
	// 删除已经解密的文件
	baDeleteFile(tfile&"02.jpg" )

end
```

通过这个过程，文件已经导入到CAST里面了。

有几点需要解释一下：

1. 文件不要在原加密文件上做解密，一定要使用文件的副本进行解密导入，以防意外情况下，素材出错，比如正在解密的时候，程序意外终止。还有，很多程序是以光盘发布的，这时候是没法在原始位置解密的。

2. 文件副本的存放，这个放在了系统的临时文件夹，你可以根据自己的实际情况选择，不过还是建议放在临时文件夹。

3. 对解密后的文件一定要及时删除。

# 拓展

1. 文件解密的代码部分是和程序一起发布出去的，我们的解密过程使用了明文密码，也就是123这个密码，你可以尝试使用baDecryptText和baEncryptText组合，弄个密文密码。因为用某些二进制工具或调试工具，纯字符串的工具很容易破解。

比如用 
```js
baDecryptText("ASDFGHJ",numtochar(21 + 46))
```
代替解密密码，相信你一定可以做的比这个复杂。

2. 你可以用改名函数把你的文件除了加密外，改成另外的文件名和扩展名，当然文件名也可以用baDecryptText和baEncryptText组合。

 
# One of Director Method for Encrypting Files

A is doing a project, there are many files, all imported into the Director, the workload is huge, and the CAST will be large, so A want to use the way of external chain material, but there is concern about file leakage.

What's the best way to solve?

Answer: If you talk about material encryption, there are many ways, for LINGO is not very skilled friends, the most convenient is the BUDAPI provides several encryption and decryption commands.

- baEncryptFile Encrypts and decrypts the file using the OR operation.  When decrypting, execute this function again with the same password, so that the file can be restored to its original appearance.

- baEncryptText encrypts String.

- The baDecryptText function decrypts String encrypted by the baEncryptText function.

# Implementation process

First, encrypt the material with the baEncryptFil function.

## Function syntax format

Note that lingo comments are "--", but md does not support lingo, here convert the comments to js "/\*... \*/", "//" expression.

```js
/*
* Parameter types：
* String，String
* FileName：Refers to the file name to be encrypted or decrypted.
* Key：Refers to a cipher string used for decryption.
*/
baEncryptFile(String, FileName, Key)
```


## Sample code
```js
on encrypt
	// This is where the material is going to be encrypted.
	tfolder=the moviepath&"image/" 
	// Find the first file that matches the specified format, in this case JPG.
	tfile=  baFindFirstFile(tfolder, "*.jpg")
	
	// The body of the loop below is to find all files in the specified format, and encrypt them.
	repeat while tfile<>"" then
		// To encrypt the file, assume the encryption password is 123
		baEncryptFile( tfile , "123" )
		// Find the next file
		tfile=baFindNextFile()
	end repeat

	// Prompt encryption complete
	alert "Done."
   end

```

Note: Before encrypting files, it is best to back up the original files.

# Use of encrypted files

The encrypted file cannot be directly imported or invoked by the Director, and must be decrypted before it can be used.

```js
on DecryptFile
	// Get the system temporary folder
	tfile=baSysFolder("temp")
	// Copy the encrypted file to a temporary folder in the system. For example, 02.jpg in the IMAGE folder in the current directory is used as an example.
	baCopyFile( the moviepath&"image/02.jpg" ,tfile&"02.jpg" , "Always" )
	// Decrypt files, note that this is to decrypt files copied to the temporary folder.
	baEncryptFile( tfile&"02.jpg" , "123")
	// Import files, here also imported files under the temporary folder.
	member(100).importFileInto(tfile&"02.jpg" )
	// Delete files that have been decrypted.
	baDeleteFile(tfile&"02.jpg" )

end
```

Through this process, the file has been imported into the CAST.

A few things need to be explained:

1. Do not decrypt the file on the original encrypted file, be sure to back up, in case of an accident, the material error, such as when decrypting, the program accidentally terminated.

2. The storage of file copies, this is placed in the temporary folder of the system, you can choose according to your actual situation, but it is still recommended to put in the temporary folder.

3. The decrypted files must be deleted in time.

# Expansion

1. The decryption code part of the file is released with the program. We decrypt the file using a plaintext password, which is the password 123. You can try using a combination of baDecryptText and baEncryptText to create a cipher. Because with some binary tools or debugging tools, pure string tools are easy to crack.

For example, use
```js
baDecryptText("ASDFGHJ",numtochar(21 + 46))
```
 instead of the decryption password,I'm sure you can do something more complicated than this.

2. You can use the rename function to change your file to a filename and extension other than the encrypted one. The filename can also be a combination of baDecryptText and baEncryptText.

# 后记/Postscript

## 说明/Description

文件由[Frank Miles Frms] (www.github.com/FrankMilesFrms) 制作，转载请注明原作者！

File by [Frank Miles Frms] (www.github.com/FrankMilesFrms), reprint please indicate the original author!

感谢[younger_z] (https://blog.csdn.net/younger_z?type=blog) 的详细技术解释，特此注明。

Thank you [younger_z] (https://blog.csdn.net/younger_z?type=blog) detailed technical explanation, hereby note.

翻译如有出入，以中文版本为解释。

If there is any discrepancy in the translation, the Chinese version shall be used for interpretation.


## 字体/Fonts

中文：聚珍方正仿宋

English：DejaVu Sans Moon

## 其他/Other

最后由FrankMilesFrms编辑于2023年8月30日。
Last edited by FrankMilesFrms on August 30, 2023.