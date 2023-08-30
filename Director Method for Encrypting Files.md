<div align="center">
The <b>English</b> version is below the <b>Chinese</b> version.
</div>

# DIRECTOR加密文件的方法之一


A在做一个项目，有很多文件，全部导入Director，工作量巨大，而且CAST会很大，所以A想用外链材料的方式，但是担心文件泄露。

最好的解决方法是什么?

答:资料加密，

# 实施过程

首先，用函数对素材加密。

注：对文件实施加密前，最好将原始文件备份。

# 加密文件的调用

被加密了的文件，Director就无法直接导入或者调用了，必须先解密后才可以使用。

通过这个过程，文件已经导入到CAST里面了。

有几点需要解释一下：

1. 文件不要在原加密文件上做解密，一定要使用文件的副本进行解密导入，以防意外情况下，素材出错，比如正在解密的时候，程序意外终止。还有，很多程序是以光盘发布的，这时候是没法在原始位置解密的。

2. 文件副本的存放，这个放在了系统的临时文件夹，你可以根据自己的实际情况选择，不过还是建议放在临时文件夹。

3. 对解密后的文件一定要及时删除。

2. 你可以用改名函数把你的文件除了加密外，改成另外的文件名和扩展名。

 
# One of Director Method for Encrypting Files

A is doing a project, there are many files, all imported into the Director, the workload is huge, and the CAST will be large, so A want to use the way of external chain material, but there is concern about file leakage.

What's the best way to solve?

Answer: If you talk about material encryption, there are many ways, for LINGO is not very skilled friends, the most convenient is the BUDAPI provides several encryption and decryption commands.

Note: Before encrypting files, it is best to back up the original files.

# Use of encrypted files

The encrypted file cannot be directly imported or invoked by the Director, and must be decrypted before it can be used.

Through this process, the file has been imported into the CAST.

A few things need to be explained:

1. Do not decrypt the file on the original encrypted file, be sure to back up, in case of an accident, the material error, such as when decrypting, the program accidentally terminated.

2. The storage of file copies, this is placed in the temporary folder of the system, you can choose according to your actual situation, but it is still recommended to put in the temporary folder.

3. The decrypted files must be deleted in time.

# 后记/Postscript

## 说明/Description

文件由[Frank Miles Frms](www.github.com/FrankMilesFrms) 制作，转载请注明原作者！

File by [Frank Miles Frms](www.github.com/FrankMilesFrms), reprint please indicate the original author!

感谢[younger_z](https://blog.csdn.net/younger_z?type=blog) 的详细技术解释，特此注明。

Thank you [younger_z](https://blog.csdn.net/younger_z?type=blog) detailed technical explanation, hereby note.

翻译如有出入，以中文版本为解释。

If there is any discrepancy in the translation, the Chinese version shall be used for interpretation.


## 字体/Fonts

中文：聚珍方正仿宋

English：DejaVu Sans Moon

## 其他/Other

最后由FrankMilesFrms编辑于2023年8月30日。
Last edited by FrankMilesFrms on August 30, 2023.
