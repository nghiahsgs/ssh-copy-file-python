# ssh-copy-file-python
ssh copy file python


```python
import os
import paramiko
from scp import SCPClient

def copy_file(mode,hostname,username,password,from_path, to_path,timeout=5000):
    ssh_client = paramiko.SSHClient()
    ssh_client.load_host_keys(os.path.expanduser(os.path.join("~", ".ssh", "known_hosts")))
    ssh_client.connect(
        hostname = hostname, 
        username = username, 
        password = password,
        timeout  = timeout,
    )

    # copy to server
    scp = SCPClient(ssh_client.get_transport())
    if mode==0:
        kq = scp.put(from_path, recursive=True, remote_path=to_path)
    # copy to local
    else:
        kq = scp.get(from_path,to_path,recursive=True)

    ssh_client.close()
    return kq

if __name__ =="__main__":
    '''
    mode = 1
    hostname  = ""
    username  = "root"
    password  = ""
    from_path = r'/root/test10'
    to_path   = ''
    copy_file(mode,hostname,username,password,from_path, to_path)
    '''


    
    # mode = 0
    # hostname  = ""
    # username  = "root"
    # password  = ""
    # from_path = r'D:\xampp\htdocs\ver3\meeypage-php\tool_upload_theme_demo_to_meeypage_aTr\sample'
    # to_path   = '/root/test10'
    # copy_file(mode,hostname,username,password,from_path, to_path)
    pass
```
