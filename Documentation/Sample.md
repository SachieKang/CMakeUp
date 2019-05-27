# Sample
#include "Markup.h"
#include <iostream>
#include <iomanip>
#include <map>
using namespace std;

typedef map<CString,CString> ccmap;
//д����
bool WriteFunc(ccmap status)
{
    CMarkup xml_CMarkup;//����xml cmark����
    xml_CMarkup.AddElem("ROOT");
    xml_CMarkup.IntoElem();
    xml_CMarkup.AddElem("HEAD");
    xml_CMarkup.IntoElem();
    xml_CMarkup.AddElem("x0",status["01"]);
    xml_CMarkup.AddElem("x1",status["02"]);
    xml_CMarkup.OutOfElem();
    xml_CMarkup.AddElem("BODY");
    xml_CMarkup.SetAttrib("id","C");//����ĳһ�������Ե�ֵ,���������֣��������ַ�
    xml_CMarkup.IntoElem();
    xml_CMarkup.AddElem("st","0");
    xml_CMarkup.AddElem("mi");
    xml_CMarkup.SetAttrib("style",1);//����ĳһ�������Ե�ֵ,���������֣��������ַ�
    xml_CMarkup.IntoElem();
    xml_CMarkup.AddElem("qs","01");
    xml_CMarkup.AddElem("cs","02");
    xml_CMarkup.AddElem("rs","03");
    xml_CMarkup.AddElem("dk","04");
    xml_CMarkup.AddElem("ls","05");
    xml_CMarkup.AddElem("pt","06");
    xml_CMarkup.AddElem("fj","07");//����Ԫ��
    xml_CMarkup.OutOfElem();
    xml_CMarkup.OutOfElem();//�˳���ǰԪ��
    CString xml_out_doc= xml_CMarkup.GetDoc();//��xmlת��Ϊ�ַ���
    std::cout<<xml_out_doc<<std::endl;
    xml_CMarkup.Save("Sample.xml");//���ļ�����Ϊxml

    return true;
}
//������
bool ReadFunction(ccmap &status)
{
    CMarkup xml_CMarkup;//����xml cmark����
    xml_CMarkup.Load("Sample.xml");//��һ���ļ���ȡxml����
    //CString xml_Doc;
    //xml_CMarkup.SetDoc(xml_Doc);//���ַ����е���xml����
    xml_CMarkup.FindElem();//�ҵ���һ���ڵ㣬�����ڵ�
    //cout<<xml_CMarkup.GetTagName();//��ȡ��ǩ����

    xml_CMarkup.IntoElem();//���뵽����ڵ�
    xml_CMarkup.FindElem("HEAD");
    xml_CMarkup.IntoElem();
    xml_CMarkup.FindElem("x0");
    MCD_STR strSN1 = xml_CMarkup.GetData();
    status.insert(pair<CString,CString>("v_head_x0",strSN1));
    xml_CMarkup.FindElem("x1");
    MCD_STR strSN2 = xml_CMarkup.GetData();
    status.insert(pair<CString,CString>("v_head_x1",strSN2));
    xml_CMarkup.OutOfElem();
    xml_CMarkup.FindElem("BODY");
    //cout<<xml_CMarkup.GetAttribName(0)<<endl;��ȡ�������ƣ�0�������һ����1����ڶ���������
    MCD_STR strSN3=xml_CMarkup.GetAttrib("id");//��ȡ����ֵ
    status.insert(pair<CString,CString>("a_body_zhunn",strSN3));
    xml_CMarkup.IntoElem();
    xml_CMarkup.FindElem("st");
    MCD_STR strSN4 = xml_CMarkup.GetData();
    status.insert(pair<CString,CString>("v_body_st",strSN4));
    xml_CMarkup.FindElem("mi");
    MCD_STR strSN5=xml_CMarkup.GetAttrib("style");//��ȡ����ֵ
    status.insert(pair<CString,CString>("a_body_mi",strSN5));
    xml_CMarkup.IntoElem();
    xml_CMarkup.FindElem("qs");
    MCD_STR strSN6 = xml_CMarkup.GetData();
    status.insert(pair<CString,CString>("v_mi_qs",strSN6));
    xml_CMarkup.ResetMainPos();//����޷�ȷ�����Ԫ�ص�˳�������ε���FindElem����֮��ʹ�ã�ʹָ�򸸽ڵ�
    xml_CMarkup.FindElem("cs");
    MCD_STR strSN7 = xml_CMarkup.GetData();
    status.insert(pair<CString,CString>("v_mi_cs",strSN7));
    xml_CMarkup.ResetMainPos();
    xml_CMarkup.FindElem("rs");
    MCD_STR strSN8 = xml_CMarkup.GetData();
    status.insert(pair<CString,CString>("v_mi_rs",strSN8));
    xml_CMarkup.ResetMainPos();
    xml_CMarkup.FindElem("dk");
    MCD_STR strSN9 = xml_CMarkup.GetData();
    status.insert(pair<CString,CString>("v_mi_dk",strSN9));
    xml_CMarkup.ResetMainPos();
    xml_CMarkup.FindElem("ls");
    MCD_STR strSN10 = xml_CMarkup.GetData();
    status.insert(pair<CString,CString>("v_mi_ls",strSN10));
    xml_CMarkup.ResetMainPos();
    xml_CMarkup.FindElem("pt");
    MCD_STR strSN11 = xml_CMarkup.GetData();
    status.insert(pair<CString,CString>("v_mi_pt",strSN11));
    xml_CMarkup.ResetMainPos();
    xml_CMarkup.FindElem("fj");
    MCD_STR strSN12 = xml_CMarkup.GetData();
    status.insert(pair<CString,CString>("v_mi_fj",strSN12));
    status.insert(pair<CString,CString>("test","test"));
    return true;
}

//������

int main()
{ 
    ccmap writeMap;
    ccmap readMap;
    ccmap::iterator iter;
    writeMap.insert(pair<CString,CString>("01","0312"));
    writeMap.insert(pair<CString,CString>("02","9999999"));
    WriteFunc(writeMap);
    ReadFunction(readMap);
    for (iter=readMap.begin();iter!=readMap.end();iter++)
    {
        cout<<setw(10)<<iter->first<<"  :   "<<iter->second<<endl;
    }
    system("pause");
    return 0;
}