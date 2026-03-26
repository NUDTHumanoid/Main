# Main

#### 资料栏
![alt text](image.png)
- wolai：https://www.wolai.com/9QZVnvSgJRw4u7EsfHqsEZ  
- Awesome humanoid robot learning：https://github.com/YanjieZe/-awesome-humanoid-robot-learning.git  
- git使用指南：https://www.bilibili.com/video/BV1Fw4m1C7Tq/?spm_id_from=333.1387.upload.video_card.click：  
- Awesome Robotics：https://github.com/kiloreux/awesome-robotics.git

#### 操作指南
注意：由于github的orginazition的空间有限制，因此，开源的只需要将代码**fork**到 **团队仓库（NUDTHumanoid）** 即可，具体步骤如下

- 拉取代码
![alt text](image-5.png)
![alt text](image-6.png)
![alt text](image-7.png)

- 本地修改
为了防止魔改后最后改不回来，所以推荐**切换分支修改**
  ```bash
  git checkout -b czy/325
  #推荐这么写，能够明确是谁修改的，然后哪一天修改的
  ```
  修改`.bashrc`显示
  ```bash
  nano .bashrc
  ```
  然后加入这段
  ```bash
  # 显示 Git 分支名称的设置
    parse_git_branch() {
        git branch 2> /dev/null | sed -e '/^[^*]/d' -e 's/* \(.*\)/(\1)/'
    }
    export PS1="\[\033[01;32m\]\u@\h\[\033[00m\]:\[\033[01;34m\]\w\[\033[00m\]\[\033[33m\]\$(parse_git_branch)\[\033[00m\]$ "
  ```
  然后执行
  ```bash
  source .bashrc
  ```
  接下来就会出现以下界面  
  ```bash
  nubot@nubot-ThinkStation-P3-Tower:~/workspace/mjlab(czy/312)$ 
  ```
  如果此刻你想知道分支有哪些(注意，这个是本地分支，如果想查看远程分支，则使用`git branch -r`,然后想切换到对应的分支，则使用`git checkout <branch>`)
  ```bash
    nubot@nubot-ThinkStation-P3-Tower:~/workspace/mjlab(czy/312)$ git branch
    czy/310
    * czy/312
    main
    #注意，*表示当前分支
  ```
  后续修改会提交到当前分支中，不会直接影响其他分支。开发完成后，将当前分支推送到远程仓库即可。
  ```
  git push origin czy/312
  ```
  ![alt text](image-4.png)

*备注：假如以前是git clone原始仓库（即`https://github.com/mujocolab/mjlab.git`），并且在原始仓库的main分支上修改，如何上传分支*
- 查看自己仓库的原始仓库
  ```bash
  git remote -v
  ```
  应该能够看到
  ```bash
  origin    https://github.com/mujocolab/mjlab.git (fetch)
  origin    https://github.com/mujocolab/mjlab.git (push)
  ```
- 增添fork的仓库
  ```bash
  git remote rename origin upstream
  git remote add origin https://github.com/NUDTHumanoid/mjlab.git
  ```
  此刻执行`git remote -v`应该会看到
  ```bash
  origin    https://github.com/NUDTHumanoid/mjlab.git (fetch)
  origin    https://github.com/NUDTHumanoid/mjlab.git (push)
  upstream  https://github.com/mujocolab/mjlab.git (fetch)
  upstream  https://github.com/mujocolab/mjlab.git (push)
  ```
 - 将自己的修改切换成新分支（假如你没有新分支是在main分支上修改的，如果你有新分支，那么直接`git push origin czy/326`即可） 
    ```bash
    git checkout -b czy/326
    #注意以后的修改就在新分支上修改，不要动main分支
    #如果想恢复main分支为初始状态，则执行
    #git switch main
    #git push origin main
    #这样你的修改就仅仅是czy/326分支指向，然后main分支恢复成最初始状态
    ```
- 然后再推动到fork的仓库中
  ```bash
  git push origin czy/326
  ``` 
  这样会基于当前main的提交创建一个新分支，后续即可将该分支推送到团队fork仓库，而不是继续直接在main上开发。