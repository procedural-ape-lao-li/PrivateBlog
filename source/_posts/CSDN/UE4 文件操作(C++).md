地址  =  文件路径  +  文件名 . 格式

1，创建文件储存内容

    FFileHelper::SaveStringToFile(内容, *地址, FFileHelper::EEncodingOptions::ForceUTF8, &IFileManager::Get(), EFileWrite::FILEWRITE_Append）);
    注：EFileWrite::FILEWRITE_Append 文件中有内容，在内容后添加；

2，写入内容

    FFileHelper::SaveStringToFile(内容, *地址, FFileHelper::EEncodingOptions::ForceUTF8);// 储存当前数据，把原有的清空

3，读取内容

    FFileHelper::LoadFileToString(存放内容变量, *地址);
   
4，判断文件是否存在

    FPaths::FileExists(地址)

5，删除文件

     PlatformFile.DeleteFile(*地址)



初步整理：仅供才考！！！
