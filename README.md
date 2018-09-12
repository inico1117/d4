# d4
#json
import json
class Student(object):
    def __init__(self,name,age,score):
        self.name=name
        self.age=age
        self.score=score
s=Student('Bob',20,88)

def student2dict(std):
    return {
        'name':std.name
        'age':std.age
        'score':std.score
    }
print(json.dumps(s,default=student2dict))

#Process
from multiprocessing import Process
import os
def run_proc(name):
    print('Run child process %s (%s)...' %(name,os.getpid()))

if __name__=='__main__':
    print('Parent process %s.' %os.getpid())
    p=Process(target=run_proc,args=('test',))
    print('Child process will start.')
    p.start()
    p.join()
    print('Child process end.')
    
#Pool
from multiprocessing import Pool
import os, time, random

def long_time_task(name):
    print('Run task %s (%s)' %(name,os.getpid()))
    start=time.time()
    time.sleep(random.random()*3)
    end=time.time()
    print('Task %s runs %0.2f seconds.' %(name,(end-start)))

if __name__=='__main__':
    print('Parent process %s.' %os.getpid())
    p=Pool(4)
    for i in range(5):
        p.apply_async(long_time_task, args=(i,))
    print('Waiting for all subprocesses done...')
    p.close()
    p.join()
    print('All subprocesses done.')
    
#threading
import time,threading

def loop():
    print('thread %s is running...' %threading.current_thread().name)
    n=0
    while n<5:
        n=n+1
        print('thread %s >>>%s' %(threading.current_thread().name,n))
        time.sleep(1)
    print('thread %s ended.' % threading.current_thread().name)

print('thread %s is running...' %threading.current_thread().name)
t=threading.Thread(target=loop,name='LoopThread')
t.start()
t.join()
print('thread %s ended.' %threading.current_thread().name)

#re.match
import re
re.match(r'^\d{3}\-\d{3,8}$', '010-12345')

#re切分字符串
re.split(r'\s+','a b  c')
re.split(r'[\s\,]+','a b,c  d')
re.split(r'[\s\,\:]+','a,b  c :d')
