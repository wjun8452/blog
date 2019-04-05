# Native crash
崩溃时系统发送信号给进程，进程的信号处理函数负责处理信号，有默认的处理函数，也可以被程序通过sigaction安装新的信号处理函数来处理。
如果系统中有两个动态库都安装了信号处理函数，则执行顺序靠后的起作用。


exception_handler.h

  // Creates a new ExceptionHandler instance to handle writing minidumps.
  // Before writing a minidump, the optional |filter| callback will be called.
  // Its return value determines whether or not Breakpad should write a
  // minidump.  The minidump content will be written to the file path or file
  // descriptor from |descriptor|, and the optional |callback| is called after
  // writing the dump file, as described above.
  // If install_handler is true, then a minidump will be written whenever
  // an unhandled exception occurs.  If it is false, minidumps will only
  // be written when WriteMinidump is called.
  // If |server_fd| is valid, the minidump is generated out-of-process.  If it
  // is -1, in-process generation will always be used.
  ExceptionHandler(const MinidumpDescriptor& descriptor,
                   FilterCallback filter,
                   MinidumpCallback callback,
                   void* callback_context,
                   bool install_handler,
                   const int server_fd);

bool IsOutOfProcess() const { return crash_generation_client_.get() != NULL; }


\#if defined(__ANDROID__)
  if (minidump_descriptor_.IsMicrodumpOnConsole())
    logger::initializeCrashLogWriter();
\#endif


