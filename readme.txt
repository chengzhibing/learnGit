git ѧϰ����


1��//���windows��û�а�װgit 
 git --version //��ʾ��ǰ�İ汾��֤����װ�ɹ���û�еĻ����ҽ̳̰�װ
2��//��װ�ɹ��ڲ˵������ҵ�Git�ļ�����Git Bash�������й���
3��//���ñ��������ֺ�����
  $ git config --global user.name "Your Name"
  $ git config --global user.email "email@example.com"
  *ע��git config�����--global���������������������ʾ����̨���������е�Git�ֿⶼ��ʹ����   �����ã���ȻҲ���Զ�ĳ���ֿ�ָ����ͬ���û�����Email��ַ��

4��//�����汾��
      ʲô�ǰ汾���أ��汾�������ֿ⣬Ӣ����repository������Լ�����һ��Ŀ¼�����Ŀ¼   ����������ļ������Ա�Git����������ÿ���ļ����޸ġ�ɾ����Git���ܸ��٣��Ա��κ�ʱ�̶�����   ׷����ʷ�������ڽ���ĳ��ʱ�̿��ԡ���ԭ����

      1�����ԣ�����һ���汾��ǳ��򵥣����ȣ�ѡ��һ�����ʵĵط�������һ����Ŀ¼��
     $ mkdir learngit
     $ cd learngit
     $ pwd
       /Users/michael/learngit
     *pwd����������ʾ��ǰĿ¼  
     *�����ʹ��Windowsϵͳ��Ϊ�˱�����������Ī����������⣬��ȷ��Ŀ¼����������Ŀ¼��           ����������
     2���ڶ�����ͨ��git init��������Ŀ¼���Git���Թ���Ĳֿ⣺
      $ git init
        Initialized empty Git repository in /Users/michael/learngit/.git/
      *˲��Git�ͰѲֿ⽨���ˣ����Ҹ�������һ���յĲֿ⣨empty Git repository����ϸ�ĵĶ���       ���Է��ֵ�ǰĿ¼�¶���һ��.git��Ŀ¼�����Ŀ¼��Git�����ٹ���汾��ģ�û��ǧ��Ҫ       �ֶ��޸����Ŀ¼������ļ�����Ȼ�����ˣ��Ͱ�Git�ֿ���ƻ��ˡ�

       �����û�п���.gitĿ¼��������Ϊ���Ŀ¼Ĭ�������صģ���ls -ah����Ϳ��Կ�����
5��//���ļ���ӵ��汾��
    1���������Ǳ�дһ��readme.txt�ļ�,�����������
       *һ��Ҫ�ŵ�learngitĿ¼�£���Ŀ¼Ҳ�У�����Ϊ����һ��Git�ֿ⣬�ŵ������ط�Git������        Ҳ�Ҳ�������ļ�
    2����һ���ļ��ŵ�Git�ֿ�ֻ��Ҫ������
       ��һ����������git add����Git�����ļ���ӵ��ֿ⣺
               $ git add readme.txt
               *ִ����������û���κ���ʾ����Ͷ���
       �ڶ�����������git commit����Git�����ļ��ύ���ֿ⣺
               $ git commit -m "wrote a readme file"
                 [master (root-commit) cb926e7] wrote a readme file
 		 1 file changed, 2 insertions(+)
 		 create mode 100644 readme.txt
               *�򵥽���һ��git commit���-m����������Ǳ����ύ��˵��������������������                ����Ȼ�����������ģ���������ܴ���ʷ��¼�﷽����ҵ��Ķ���¼
               *git commit����ִ�гɹ��������㣬1���ļ����Ķ�����������ӵ�readme.txt�ļ�                 ���������˼������ݣ�readme.txt������������ݣ�
               *ΪʲôGit����ļ���Ҫadd��commitһ�������أ���Ϊcommit����һ���ύ�ܶ��ļ�		����������Զ��add��ͬ���ļ������磺

		$ git add file1.txt
		$ git add file2.txt file3.txt
		$ git commit -m "add 3 files."
6��//�ļ�״̬������
   �����Ѿ��ɹ�����Ӳ��ύ��һ��readme.txt�ļ������ڣ���ʱ����������ˣ����ǣ����Ǽ����޸�    readme.txt�ļ�������������ģ�
    1�����ڣ�����git status��������
        $ git status
	# On branch master
	# Changes not staged for commit:
	#   (use "git add <file>..." to update what will be committed)
	#   (use "git checkout -- <file>..." to discard changes in working directory)
	#
	#    modified:   readme.txt
	#
	no changes added to commit (use "git add" and/or "git commit -a")
       *git status�������������ʱ�����ղֿ⵱ǰ��״̬�����������������ǣ�readme.txt����          �Ĺ��ˣ�����û��׼���ύ���޸ġ�
   2����ȻGit��������readme.txt���޸��ˣ�������ܿ��������޸���ʲô���ݣ���Ȼ�Ǻܺõġ�����      ���ݼ����ܴӹ����������һ���ϰ�ʱ���Ѿ��ǲ����ϴ���ô�޸ĵ�readme.txt�����ԣ���Ҫ��        git diff����������
     	$ git diff readme.txt 
	diff --git a/readme.txt b/readme.txt
	index 46d49bf..9247db6 100644
	--- a/readme.txt
	+++ b/readme.txt
	@@ -1,2 +1,2 @@
	-Git is a version control system.
	+Git is a distributed version control system.
 	Git is free software.
7��//�汾���ˣ�
   1��git log������ʾ���������Զ���ύ��־������������Ϣ̫�࣬�����ۻ����ҵģ��������Լ�          ��--pretty=oneline������
   $ git log --pretty=oneline
     3628164fb26d48395383f8f31179f24e0882e1e0 append GPL
     ea34578d5496d7dd233c827ed32a8cd576c5ee85 add distributed
     cb926e7ea50ad11b8f9e909c05226233bf755030 wrote a readme file
     *3628164...882e1e0��commit id���汾�ţ�
   2��git reset --hard HEAD  �鿴��ǰ�汾
      git reset --hard HEAD^ ��һ���汾
      git reset --hard HEAD^^�������汾
      git reset --hard HEAD~100��100���汾
      $ git reset --hard 3628164���⴮����Ϊ�汾�ţ���ת����Ӧ�汾
      $ git reflog  Git�ṩ��һ������git reflog������¼���ÿһ�����
	ea34578 HEAD@{0}: reset: moving to HEAD^
	3628164 HEAD@{1}: commit: append GPL
	ea34578 HEAD@{2}: commit: add distributed
	cb926e7 HEAD@{3}: commit (initial): wrote a readme file
      �����Բ鿴���������İ汾�ţ�
   