
ע������ʹ�õ�������lxmertģ�͵õ��ĸ�query id ������product�ļ���val.txt��test.txt������ѵ���׶����ɣ�
ÿѵ��һ�ֶ��ᱣ���epoch�µ�ģ���Լ���ģ�Ͳ�����val.txt�Լ�test.txt��ͬʱҲ�ṩ���Խӿڣ���ȡѵ�����
��ģ�ͣ�����val.txt��test.txt��

����lxmertģ�͵�ѵ���Ͳ��Խű�bash·���޸ĵ�˵����

����ִ��prepare�ļ��� python prepare.py

һ. ѵ���׶�

1.1 �л���lxmert��Ŀ¼�£����ն�ִ�� bash run/train.bash 0 lxr_model
���У�
lxr_modelΪ���浱��ѵ�������ģ�ͣ���־�ȣ����ļ������ƣ����޸�Ϊ�������ƣ����ɳ����Զ����ɸ��ļ��С�

1.2 �޸���Ŀ¼��eval.py�У�131�е�standard_path·��Ϊʵ��valid_answer.json·����

1.3 �޸�run/train.bash�е�·����
���У�
--loadLXMERTQA   Ϊ pretrain_path/model  pretrain_pathΪԤѵ��ģ��model_LXRT.pth���ϼ�Ŀ¼��ע���·��û������
--basedatadir   Ϊ����Ŀ¼�������˴�����train.tsv, valid.tsv ��testB.tsv
--basebert    Ϊbert-base-uncased.tar.gz��·��
--RESUME ��--path_checkpoint    Ϊ��ѵ���ܣ�--RESUMEȱʡΪ0����ֵΪ1��ʱ��������ѵ����ʱ����--path_checkpointΪ
user_data/lxmert_model/checkpoint/�ļ�����lxr_best.pth��·��


1.4 ѵ��
beike1~beike12�ֱ����������µ�ѵ���趨����Ҫ�޸ĵ�bash��������


beike1    lr = 6e-5  max_box =5 ѵ��16��
beike2    lr = 6e-5  max_box =5 ѵ��19��
beike3    lr = 5e-5  max_box =5 ѵ��15��
beike4    lr=6e-5    max_box = 20 ѵ��24��
beike5    lr=6e-5    max_box =5   ѵ��30��
beike6    lr=6e-5   max_box = 20 ѵ��30��
beike7    lr=6e-5    max_box =5   ѵ��32��
beike8    lr=6e-5    max_box =5   ѵ��33��
beike9   lr=6e-5    max_box =5   ѵ��34��

beike10��finetune��25��max_box =5��������ROI Select���� �ĵ�31��
beike11��finetune��25��max_box =5��������ROI Select���� �ĵ�32��
beike12��finetune��25��max_box =5��������ROI Select���� �ĵ�33��

ѵ�����
beike1:  ִ�����bash run/beike1.bash 0 beike1
beike2:  ִ�����bash run/beike2.bash 0 beike2
beike3:  ִ�����bash run/beike3.bash 0 beike3
beike4:  ִ�����bash run/beike4.bash 0 beike4
beike5:  ִ�����bash run/beike5.bash 0 beike5
beike6:  ִ�����bash run/beike6.bash 0 beike6
beike7:  ִ�����bash run/beike7.bash 0 beike7
beike8:  ִ�����bash run/beike8.bash 0 beike8
beike9:  ִ�����bash run/beike9.bash 0 beike9
beike10:  ִ�����1. bash run/beike101112_finetune.bash 0 beike10
                               2.bash run/beike10.bash 0 beike10
beike11:  ִ�����1. bash run/beike101112_finetune.bash 0 beike11
                               2.bash run/beike11.bash 0 beike11
beike12:  ִ�����1. bash run/beike101112_finetune.bash 0 beike12
                               2.bash run/beike12.bash 0 beike1


��. ���Խ׶�
ʵ������ѵ����ʱ��ÿһ�ֶ���������Ӧ��test.txt��val.txt������ֻ�����ṩһ�����������Ĳ��Խӿڡ�
�������beike1.pth��ʱ��ֻ��Ҫ��lxmertĿ¼��ִ�� bash run/test.bash

���У�test.bash���£�
result_output=../../user_data/lxmert_model/result
mkdir -p $result_output/val
mkdir -p $result_output/test

CUDA_VISIBLE_DEVICES=0
    python src/tasks/get_prob.py \
    --test testB  --valid valid \
    --basedatadir '../../user_data/lxmert_processfile/' \
    --basebert '../../external_resources/pretrained/bert/bert-base-uncased.tar.gz' \
    --load '../../user_data/lxmert_model/beike1/beike1.pth' \
    --name 'beike1' \

    
���Ҫ����beike2.pth,ֻ���޸Ķ�Ӧ�����Ƽ��ɣ� bash run/test.bash

��ʱ��test.bash���£�

result_output=../../user_data/lxmert_model/result
mkdir -p $result_output/val
mkdir -p $result_output/test

CUDA_VISIBLE_DEVICES=0
    python src/tasks/get_prob.py \
    --test testB  --valid valid \
    --basedatadir '../../user_data/lxmert_processfile/' \
    --basebert '../../external_resources/pretrained/bert/bert-base-uncased.tar.gz' \
    --load '../../user_data/lxmert_model/beike2/beike2.pth' \
    --name 'beike2' \




