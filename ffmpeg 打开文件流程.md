# ffmpeg 打开文件流程

- avformat_open_input 打开文件，调用avformat_alloc_context
- avformat_alloc_context： 创建AVFormatContext，调用avformat_get_context_defaults
- avformat_get_context_defaults： 设置 s->io_open  = io_open_default;
- io_open_default调用 ffio_open_whitelist
- ffio_open_whitelist ： 调用ffurl_open_whitelist查找协议，ffio_fdopen打开协议
- ffio_fdopen调用avio_alloc_context，read_packet指针参数为io_read_packet
- io_read_packet ：调用ffurl_read
- ffurl_read ： 调用retry_transfer_wrapper
- retry_transfer_wrapper：调用transfer_func
- transfer_func : 调用h->prot->url_read，即 URLContext-->URLProtocol-->url_read



# ffmpeg读文件流程

- av_read_frame
-  read_frame_internal
-  ff_read_packet
-  s->iformat->read_packet ---> mov_read_packet
-  av_get_packet
-  avio_read
-  s->read_packet
-  ffurl_read 
-  retry_transfer_wrapper --> h->prot->url_read
-  file_read

![image-20190109134451325](/Users/xzl/Library/Application Support/typora-user-images/image-20190109134451325.png)