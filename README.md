# Infix-to-Postfix

## Convert Infix expression to Postfix expression using Stack

#include <iostream>
#include<string.h>
using namespace std;

class Stack
{
public:
    int size;
    int top;
    char *s;
};

void push(Stack *st,char x)
{
    if(st->top==st->size-1)
    {
        cout<<"Stack Overflow"<<endl;
    }
    else
    {
        st->top++;
        st->s[st->top]=x;
    }
}

char pop(Stack *st)
{
    char x='-1';
    if(st->top==-1)
    {
        cout<<"Stack Underflow"<<endl;
    }
    else
    {
        x=st->s[st->top];
        st->top--;
    }
    return x;
}

int isEmpty(Stack st)
{
    if(st.top==-1)
    {
        return 1;    
    }
    else
    {
        return 0;
    }
}

char stackTop(Stack st)
{
    char x='-1';
    if(st.top==-1)
    {
        return x;
    }
    else
    {
        x=st.s[st.top];
        return x;
    }
}

int isOperand(char x)
{
    if(x=='+' || x=='-' || x=='*' || x=='/')
    {
        return 0;
    }
    else
    {
        return 1;
    }
}

int pre(char x)
{
    if(x=='+' || x=='-')
    {
        return 1;
    }
    else if(x=='*' || x=='/')
    {
        return 2;
    }
    else
    {
        return 0;
    }
}

char* convert(char *infix)
{
    Stack st;
    st.size=strlen(infix);
    st.top=-1;
    st.s=new char[st.size];
    char *postfix=new char[st.size+1];
    int i=0,j=0;
    while(infix[i]!='\0')
    {
        if(isOperand(infix[i]))
        {
            postfix[j]=infix[i];
            j++;i++;
        }
        else
        {
            if(pre(infix[i])>pre(stackTop(st)))
            {
                push(&st,infix[i]);
                i++;
            }
            else
            {
                postfix[j]=pop(&st);
                j++;
            }
        }
    }
    while(!isEmpty(st))
    {
        postfix[j]=pop(&st);
        j++;
    }
    postfix[j]='\0';
    return postfix;
}

int main()
{
    char infix[20];
    cout<<"Enter Expression: ";
    cin>>infix;
    cout<<"Postfix Expression is: "<<convert(infix)<<endl;
    return 0;
}
