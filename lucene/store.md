# store(存储)

这层的目的是数据交换层，目的是承上启下，对上层透明数据的存储和读取，对下层透明数据的编码和组织。分层很重要啊。

`Directory`作为文件目录的抽象类，你可以理解成为文件系统的一个目录，虽然实际上并不能这么简单认为，因为文件不只是可以放在文件系统中，也可以在内存中，在分布式文件系统，在三体空间中... 。里面有几个重要的方法要提下：

1. `String[] listAll()`返回索引文件目录下的所有文件
1. `IndexOutput createOutput(String name, IOContext context)`创建指定名称的新文件（这里再强调下，虽然我说了*文件*两字，但是不要直接理解成文件系统的文件）。注意返回的`IndexOutput`实例是非线程安全的，所以任何一个文件的写操作必需在一个线程内。
1. `IndexInput openInput(String name, IOContext context)`和`createOutput`相反，读取索引文件。无论是IndexOutput还是IndexIntput，操作的都是索引文件最底层的数据，比如写入读取 int，string，不负责索引的编码协议之类，如B树结构，Lucene4x还是Lucene50格式。

