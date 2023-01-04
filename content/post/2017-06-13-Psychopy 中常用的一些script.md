---
title: Psychopy 中常用的一些script
author: yuanbo
date: 2017-06-13
slug: psychopy-scripts
category:   
tags: 
show_toc: true
---

#


real_exp_feedback=u"本轮中你选择了$f_num 次'f'键，$j_num 次‘j’键，本轮你得到$f_num*0.1元+$j_num*0.01元。 \n\n按空格键继续实验！"

practice_total = f_num*0.1 + j_num*0.01
practice_feedback = u"你选择了 %.0f 次F键，" %f_num  + u"选择了 %.0f 次J键。" %j_num + u"\n\n你共得到 %.0f *0.1元 +" %f_num + u" %.0f *0.01元," %j_num + u"共计 %.2f 元" % practice_total + u"\n\n按空格键继续实验。"


#  根据正确错误给予反馈
```
feedbackText=""

if popped==True:
  feedbackText="Oops! Lost that one!"
  bang.play()
else:
  feedbackText=u"You banked £%.2f" %lastBalloonEarnings
  
```


#  msg variable just needs some value at start

msg=''

if resp.corr:#stored on last run routine
  msg="Correct! RT=%.3f" %(resp.rt)
else:
  msg="Oops! That was wrong"

# 图形显示被试的数据结果
from matplotlib import pyplot
import pandas as pd

def plotYX(yaxis, xaxis, description=''):
    pyplot.grid(True)
    pyplot.title(description)
    pyplot.xlabel('Angle')
    pyplot.ylabel('Response time (s)')
    pyplot.xlim([0, 315])
    #slope,inter = np.polyfit(xaxis[:5],yaxis[:5],1)
    pyplot.plot(xaxis, yaxis) #, xaxis[:5], np.array(xaxis[:5]) * slope + inter)
    pyplot.draw()
    pyplot.show()

filename = 'mental_rotation_data.csv'
with open(filename, 'wb') as fd:
    fd.write(data_string)

data = pd.read_csv(filename)
data = data[data['rt'] < 4]  # trim RT at 4 sec
mrt = data.loc[:,'rt']
correct = data.loc[:, 'corr']
angle = data.loc[:, 'angle']

dfsum = data.groupby('angle', as_index=False).mean()
m = dfsum.loc[:, 'rt']
a = dfsum.loc[:, 'angle']

scored_data = zip(a, m)
print 'average time (sec) at each rotation:'
print "  0  45  90  135 180 225 270 315"
print "--> %s <--" % repr([round(i,3) for i in m]).strip('[]').replace(',', '  ')
print "\n% correct        :", 100 * correct.mean()
print "overall speed (s):", mrt.mean()

plotYX(m, a)

with open(filename, 'a+b') as fd:
    fd.write('\n\n' + repr(scored_data))