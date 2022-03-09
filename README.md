#include<stdio.h>
#include<stdlib.h>
#include<string.h>

typedef struct stu
{
    int num;
    char name[20];
    int math;
    int chinese;
    int english;
    int physic;
    int history;
    int zongfen;
    struct stu *next;
}message;

int main()
{
    message *creat(message *head);
    message *zongf(message *head);
    message *paixu1(message *head);
    message *paixu2(message *head);
    message *dele(message *head);
    message *insert(message *head);
    void search (message *head);
    void print1(message *head);
    void print2(message *head);
    message *head=NULL;
    message *zscore=NULL;
    
    printf("          欢 迎 使 用 本 成 绩 管 理 系 统\n");
    printf("              菜                 单\n");
    printf("                1.输入学生信息\n");
    printf("                2.输出学生信息\n");
    printf("                3.计算所有学生总成绩并输出(必须先执行操作1)\n");
    printf("                4.将所有学生总成绩排名(必须先进行操作1和操作3)\n");
    printf("                5.按学号输出学生总成绩\n");
    printf("                6.查询学生成绩\n");
    printf("                7.删除学生成绩\n");
    printf("                8.插入学生成绩\n");
    printf("                9.退出\n");
    
    int cz=1;
    while (cz!=0)
    {
        printf("            请 选 择 您 要 进 行  的 操 作\n");
        scanf("%d",&cz);
        switch (cz)
        {
        case 1:
        head=creat(head);
        break;
        
        case 2:
        print1(head);
        break;
        
        case 3:
        head=zongf(head);
        print2(head);
        break;
        
        case 4:
        head=paixu1(head);
        print2(head);
        break;
        
        case 5:
        head=paixu2(head);
        print2(head);
        break;

        case 6:
        search(head);
        break;

        case 7:
        head=dele(head);
        break;

        case 8:
        head=insert(head);
        break;

        case 9:
        goto A; //跳出循环
        }
    }
    
A:
    printf("谢谢使用!\n");
    system("pause");
    return 0;

}

#if(1)

message *creat(message *head)
{
    message *q,*p;
    int ch=1;
    while(ch!=0)
    {
        q=(struct stu *)malloc(sizeof(struct stu));
        printf("请输入学生的学号 姓名  (成绩)数学 语文 英语 物理 历史(输入0结束)：\n");
        scanf("%d%s%d%d%d%d%d",&q->num,q->name,&q->math,&q->chinese,
                                &q->english,&q->physic,&q->history);
        ch=q->num;
        if(ch!=0)
        {
            q->next=NULL;
            if(head==NULL)
            {
                head=q;
            } else
            {
                p->next=q;
            }
            p=q;
        }
    }
    return head;
}
#endif

#if(1)
message *zongf(message *head)
{
    message *q=head;
    while (q!=NULL)
    {
        q->zongfen=q->math+q->chinese+q->english+q->history+q->physic;
        q=q->next;
    }
    return head;
}

#endif

#if(1)

message *paixu2(message *head)
{
    message *q,*p,*p1;
    int xh,zscore;
    char a[20];
    q=head;
    while (q!=NULL)
    {
        p=q->next;
        while (p!=NULL)
        {
            if(q->num > p->num)
            {
                xh=q->num;
                q->num=p->num;
                p->num=xh;

                strcpy(a,q->name);
                strcpy(q->name,p->name);
                strcpy(p->name,a);

                zscore=q->zongfen;
                q->zongfen=p->zongfen;
                p->zongfen=zscore;
            }
            p=p->next;
        }
        q=q->next;
        
    }
    return head;
}

#endif

#if(1)
message *paixu1(message *head)
{
    message *q,*p,*p1;  
    char a[20];
    int xh,zscore;
    q=head;
    while (q!=NULL)
    {
        p=q->next;
        while (p!=NULL)
        {
            if(q->zongfen < p->zongfen)
            {
                xh=q->num;
                q->num=p->num;
                p->num=xh;

                strcpy(a,q->name);
                strcpy(q->name,p->name);
                strcpy(p->name,a);
                
                zscore=q->zongfen;
                q->zongfen=p->zongfen;
                p->zongfen=zscore;
            }
            p=p->next;
        }
        q=q->next;
    }
    return head;
    
}

#endif

#if(1)
void search(message *head)
{
    message *p;
    char name[20];
    int a;
    
    B:
        printf("请输入您要查找的学生姓名:\n");
        scanf("%s",&name);
        p=head;
        while (p!=NULL && strcmp(p->name,name)!=0)
        {
            p=p->next;
        }
        
        if(p)
        {
            printf("学号\t姓名\t(成绩)数学\t语文\t英语\t物理\t历史\n");
            printf("%d\t%s\t\t%d\t%d\t%d\t%d\t%d\n",p->num,p->name,p->math,
                p->chinese,p->english,p->physic,p->history);
        }else
        {
            printf("没有%s同学的信息!\n",name);
        }
        printf("查找成功!\n");
        printf("是否继续查找：yes(1)/no(0)\n");
        scanf("%d",&a);
        while(a)
        {
            if(a==1)
            {
                goto B;
            }else if(a==0)
            {
                printf("关闭查找功能!\n");
            }else
            {
                printf("输入错误，请重新输入:\n");
                scanf("%d",&a);
            }
        }
}

#endif

#if(1)
void print1(message *head)
{
    message *p=head;
    printf("学号\t\t姓名\t\t语文\t数学\t英语\t物理\t化学\n");
    while(p!=NULL)
    {
        printf("%d\t%10s\t\t%d\t%d\t%d\t%d\t%d\n",p->num,p->name,p->math,
                p->chinese,p->english,p->physic,p->history);
        p=p->next;
    }
}

#endif


#if(1)
void print2(message *head)
{
    message *p=head;
    printf("学号\t姓名\t总成绩\n");
    while (p!=NULL)
    {
        printf("%d\t%s\t%d\n",p->num,p->name,p->zongfen);
        p=p->next;
    }
}

#endif

#if(1)
message *dele(message *head)
{
    struct stu *q,*p;
    char name[20];
    int a;
    q=head;

C:
    printf("请输入您要删除的学生姓名：\n");
    scanf("%s",&name);
    while (q!=NULL && strcmp(q->name,name)!=0)
    {
        p=q;
        q=q->next;
    }
    if(q==NULL)
    {
        printf("没有%s同学的成绩信息!\n",name);
    }else if(q==head)
    {
        head=p->next;
    }else
    {
        p->next=q->next;
    }
    printf("删除成功!\n");
    printf("是否继续删除:yes(1)/no(0)\n");
    scanf("%d",&a);
    while (a)
    {
        if (a==1)
        {
            goto C;
        }else if(a==0)
        {
            printf("关闭删除功能!\n");
        }else
        {
            printf("输入错误，请重新输入:\n");
            scanf("%d",&a);
        }
    }
    free(q);
    return head;
}

#endif

#if(1)
message *insert(message *head)
{
    message *q,*p,*p1;
    int a;

D:
    q=(struct stu *)malloc(sizeof(struct stu));
    printf("请输入学生的学号 姓名  (成绩)数学 语文 英语 物理 历史(输入0结束)：\n");
    scanf("%d%s%d%d%d%d%d",&q->num,q->name,&q->math,&q->chinese,
                            &q->english,&q->physic,&q->history);
    if(head==NULL)
    {
        q->next=NULL;
        head=q;
        return head;
    }
    if(head->num > q->num)
    {
        q->next=head;
        head=q;
        return head;
    }
    p=head;
    p1=head->next;
    while (p1!=NULL && p1->num < q->num)
    {
        p=p1;
        p1=p1->next;
    }
    q->next=p1;
    p->next=q;
    printf("插入成功!\n");
    printf("是否继续插入：yes(1)/no(0)\n");
    scanf("%d",&a);
    while (a)
    {
        if (a==1)
        {
            goto D;
        }else if (a==0)
        {
            printf("关闭插入功能!");
        }else
        {
            printf("输入错误，请重新输入：\n");

            scanf("%d",&a);
        }
        
    }
    return head;
    
}

#endif
