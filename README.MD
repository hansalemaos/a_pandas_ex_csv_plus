# When pd.read_csv(csvstring, sep='\s+') doesn't work ... 

```python
pip install a-pandas-ex-csv-plus
```

```python
from a_pandas_ex_csv_plus import pd_add_convert_to_df
pd_add_convert_to_df()
import pandas as pd
xaxa='''
2020-09-1022-30-03.mp4   2020-10-08 18-54-44.mp4   2020-10-14 19-46-34.mp4
2020-09-1022-30-10.mp4   2020-10-08 18-56-39.mp4   2020-10-17 12-11-54.mp4
2020-09-1022-30-13.mp4                            2020-10-17 13-23-56.mp4
2020-09-1022-30-33.mp4                           
2020-09-1022-30-38.mp4                           
2020-09-1022-30-41.mp4                            2020-10-17 13-30-27.mp4
2020-09-1022-31-03.mp4   2020-10-1115-49-19.mp4   2020-10-17 13-30-28.mp4
2020-09-1022-31-36.mp4   2020-10-1116-10-45.mp4   2020-10-17 13-30-41.mp4
                        2020-10-11 16-34-20.mp4   acesseoscursos.mp4
                        2020-10-1116-48-08.mp4    acesseoscursoscelular.mp4
                        2020-10-11 19-00-47.mp4    reaberturatrailer.mp4
                        2020-10-1119-08-19.mp4   rexmega.mp4
2020-10-0818-54-37.mp4  2020-10-1119-17-33.mp4
'''
## Pure Pandas - probably not what you want:

print(pd.read_csv(StringIO(xaxa), sep=r'\s+', on_bad_lines='skip').to_string())
    2020-09-1022-30-03.mp4                 2020-10-08           18-54-44.mp4    2020-10-14  19-46-34.mp4
0   2020-09-1022-30-10.mp4                 2020-10-08           18-56-39.mp4    2020-10-17  12-11-54.mp4
1   2020-09-1022-30-13.mp4                 2020-10-17           13-23-56.mp4           NaN           NaN
2   2020-09-1022-30-33.mp4                        NaN                    NaN           NaN           NaN
3   2020-09-1022-30-38.mp4                        NaN                    NaN           NaN           NaN
4   2020-09-1022-30-41.mp4                 2020-10-17           13-30-27.mp4           NaN           NaN
5   2020-09-1022-31-03.mp4     2020-10-1115-49-19.mp4             2020-10-17  13-30-28.mp4           NaN
6   2020-09-1022-31-36.mp4     2020-10-1116-10-45.mp4             2020-10-17  13-30-41.mp4           NaN
7               2020-10-11               16-34-20.mp4     acesseoscursos.mp4           NaN           NaN
8   2020-10-1116-48-08.mp4  acesseoscursoscelular.mp4                    NaN           NaN           NaN
9               2020-10-11               19-00-47.mp4  reaberturatrailer.mp4           NaN           NaN
10  2020-10-1119-08-19.mp4                rexmega.mp4                    NaN           NaN           NaN
11  2020-10-0818-54-37.mp4     2020-10-1119-17-33.mp4                    NaN           NaN           NaN

df = pd.Q_convert_to_df(string_table=xaxa, regex_sep=r"\s+", tolerance=1)
print(df.to_string())
                         0                        2                          3
0   2020-09-1022-30-03.mp4  2020-10-08 18-54-44.mp4    2020-10-14 19-46-34.mp4
1   2020-09-1022-30-10.mp4  2020-10-08 18-56-39.mp4    2020-10-17 12-11-54.mp4
2   2020-09-1022-30-13.mp4                             2020-10-17 13-23-56.mp4
3   2020-09-1022-30-33.mp4                                                    
4   2020-09-1022-30-38.mp4                                                    
5   2020-09-1022-30-41.mp4                             2020-10-17 13-30-27.mp4
6   2020-09-1022-31-03.mp4   2020-10-1115-49-19.mp4    2020-10-17 13-30-28.mp4
7   2020-09-1022-31-36.mp4   2020-10-1116-10-45.mp4    2020-10-17 13-30-41.mp4
8                           2020-10-11 16-34-20.mp4         acesseoscursos.mp4
9                            2020-10-1116-48-08.mp4  acesseoscursoscelular.mp4
10                          2020-10-11 19-00-47.mp4      reaberturatrailer.mp4
11                           2020-10-1119-08-19.mp4                rexmega.mp4
12  2020-10-0818-54-37.mp4   2020-10-1119-17-33.mp4                           


xaxa2 = """
com.blues  2003     system  mem   unknown                                         /dev/ashmem/dalvik-LinearAlloc (deleted)
com.blues  2003     system  mem       CHR              10,60                 7622 /dev/binder
com.blues  2003     system  mem   unknown                                         /dev/ashmem/dalvik-indirect ref table (deleted)
com.blues  2003     system  mem   unknown                                         /dev/ashmem/dalvik-allocspace zygote / non moving space live-bitmap 0 (deleted)
com.blues  2003     system  mem       REG                8,1   8774704     263011 /system/lib/libart.so
com.blues  2003     system  mem       REG                8,1     29176     263435 /system/fonts/NotoSansLao-Bold.ttf
com.blues  2003     system  mem       REG                8,1    411120     262703 /system/lib/libinputflinger.so
com.andro 19725     u0_a54  cwd       DIR                0,2       820          2 /
com.andro 19725     u0_a54  rtd       DIR                0,2       820          2 /
com.andro 19725     u0_a54  txt       REG                8,1     17948     262260 /system/bin/app_process32
com.andro 19725     u0_a54  mem   unknown                                         /dev/ashmem/dalvik-main space (deleted)
com.andro 19725     u0_a54  mem   unknown                                         /dev/ashmem/dalvik-main space 1 (deleted)
com.andro 19725     u0_a54  mem       REG               8,17   2125824    2228227 /data/dalvik-cache/x86/system@framework@boot.art
com.andro 19725     u0_a54  mem       REG               8,17   1167360    2228229 /data/dalvik-cache/x86/system@framework@boot-core-libart.art
com.andro 19725     u0_a54  mem       REG                8,1      5142     263912 /system/usr/hyphen-data/hyph-mn-cyrl.hyb
com.andro 19725     u0_a54  mem       REG                8,1     35913     263879 /system/usr/hyphen-data/hyph-cy.hyb
com.andro 19725     u0_a54  mem   unknown                                         /dev/ashmem/dalvik-large object space allocation (deleted)
com.andro 19725     u0_a54  mem       REG                8,1     67076     262937 /system/lib/libkeymaster_messages.so
com.andro 19725     u0_a54  mem       REG                8,1    202252     262648 /system/lib/libkeymaster1.so
com.andro 19725     u0_a54  mem       REG                8,1    160904     262967 /system/lib/libsoftkeymasterdevice.so
com.andro 19725     u0_a54  mem       REG                8,1    156172     262657 /system/lib/libjavacrypto.so
com.andro 19725     u0_a54  mem       REG                8,1    124456     263004 /system/lib/libkeystore_binder.so
com.andro 19725     u0_a54  mem   unknown                                         /dev/ashmem/dalvik-large object space allocation (deleted)
com.andro 19725     u0_a54  mem   unknown                                         /dev/ashmem/dalvik-large object space allocation (deleted)
com.andro 19725     u0_a54  mem   unknown                                         /dev/ashmem/dalvik-large object space allocation (deleted)
com.andro 19725     u0_a54  mem       REG               0,15    131072       6346 /dev/__properties__/u:object_r:logd_prop:s0
com.andro 19725     u0_a54  mem       REG               0,15    131072       6339 /dev/__properties__/u:object_r:default_prop:s0
com.andro 19725     u0_a54  mem       REG                8,1      8165     263886 /system/usr/hyphen-data/hyph-fr.hyb
com.andro 19725     u0_a54  mem   unknown                                         /dev/ashmem/dalvik-large object space allocation (deleted)
com.andro 19725     u0_a54  mem       REG                8,1       607     263890 /system/usr/hyphen-data/hyph-pa.hyb
com.andro 19725     u0_a54  mem       REG                8,1      9716     262949 /system/lib/libkeystore-engine.so
com.andro 19725     u0_a54  mem       REG                8,1       647     263924 /system/usr/hyphen-data/hyph-or.hyb
com.andro 19725     u0_a54  mem   unknown                                         /dev/ashmem/dalvik-large object space allocation (deleted)
com.andro 19725     u0_a54  mem       REG                8,1    518036     262595 /system/lib/libmedia_jni.so
com.andro 19725     u0_a54  mem       REG                8,1    202168     263023 /system/lib/libexif.so
com.andro 19725     u0_a54  mem       REG                8,1    136632     262593 /system/lib/libmtp.so
com.andro 19725     u0_a54  mem       REG                8,1     71116     263050 /system/lib/libstagefright_amrnb_common.so
com.andro 19725     u0_a54  mem       REG                8,1       687     263891 /system/usr/hyphen-data/hyph-mr.hyb
com.andro 19725     u0_a54  mem       REG               0,15    131072       6352 /dev/__properties__/u:object_r:log_prop:s0
com.andro 19725     u0_a54  mem   unknown                                         /dev/ashmem/dalvik-large object space allocation (deleted)
com.andro 19725     u0_a54  mem       REG                8,1    504430     263754 /system/usr/share/zoneinfo/tzdata
com.andro 19725     u0_a54  mem       REG                8,1  18677700     263362 /system/fonts/NotoSansCJK-Regular.ttc
com.andro 19725     u0_a54  mem       REG                8,1      6967     263882 /system/usr/hyphen-data/hyph-da.hyb
com.andro 19725     u0_a54  mem   unknown                                         /dev/ashmem/dalvik-large object space allocation (deleted)
com.andro 19725     u0_a54  mem   unknown                                         /dev/ashmem/dalvik-large object space allocation (deleted)
com.andro 19725     u0_a54  mem       REG                8,1     40308     263449 /system/fonts/CarroisGothicSC-Regular.ttf
com.andro 19725     u0_a54  mem       REG                8,1  22201456     263865 /system/usr/icu/icudt56l.dat
com.andro 19725     u0_a54  mem   unknown                                         /dev/ashmem/dalvik-LinearAlloc (deleted)
com.andro 19725     u0_a54  mem       REG               8,17   1663816    2228313 /data/dalvik-cache/x86/system@app@PrintSpooler@PrintSpooler.apk@classes.dex
com.andro 19725     u0_a54  mem   unknown                                         /dev/ashmem/dalvik-indirect ref table (deleted)
com.andro 19725     u0_a54  mem   unknown                                         /dev/ashmem/dalvik-indirect ref table (deleted)
com.andro 19725     u0_a54  mem       REG                8,1   4912800     262602 /system/lib/libart-compiler.so
com.andro 19725     u0_a54  mem       REG                8,1   1232260     262969 /system/lib/libvixl.so
com.andro 19725     u0_a54  mem       REG                8,1  22201456     263865 /system/usr/icu/icudt56l.dat
com.andro 19725     u0_a54  mem   unknown                                         /dev/ashmem/dalvik-Jit thread pool worker thread 0 (deleted)
com.andro 19725     u0_a54  mem       CHR              10,60                 7622 /dev/binder
com.andro 19725     u0_a54  mem   unknown                                         /dev/ashmem/dalvik-allocspace zygote / non moving space live-bitmap 0 (deleted)
com.andro 19725     u0_a54  mem       REG                8,1   8774704     263011 /system/lib/libart.so
com.andro 19725     u0_a54  mem       REG                8,1     29176     263435 /system/fonts/NotoSansLao-Bold.ttf
com.andro 19725     u0_a54  mem       REG                8,1    411120     262703 /system/lib/libinputflinger.so
com.andro 19725     u0_a54  mem       REG                8,1     42532     262665 /system/lib/libnativeloader.so
com.andro 19725     u0_a54  mem       REG                8,1     30228     262758 /system/lib/libhardware_legacy.so
com.andro 19725     u0_a54  mem       REG                8,1     46512     263059 /system/lib/libRS.so
"""

# Pure Pandas - probably not what you want:

print(pd.read_csv(StringIO(xaxa2), sep=r'\s+', on_bad_lines='skip').to_string())
           com.blues    2003 system      mem                         unknown /dev/ashmem/dalvik-LinearAlloc    (deleted)
com.blues       2003  system    mem      CHR                           10,60                           7622  /dev/binder
com.andro      19725  u0_a54    mem  unknown         /dev/ashmem/dalvik-main                          space    (deleted)
com.andro      19725  u0_a54    mem  unknown  /dev/ashmem/dalvik-LinearAlloc                      (deleted)          NaN
com.andro      19725  u0_a54    mem      CHR                           10,60                           7622  /dev/binder


df2 = pd.Q_convert_to_df(string_table=xaxa2, regex_sep=r"\s+", tolerance=1)
print(df2.to_string())

           0      1       6    8        11     25        27       31                                                                               32
0   com.blues   2003  system  mem  unknown                                                                   /dev/ashmem/dalvik-LinearAlloc (deleted)
1   com.blues   2003  system  mem      CHR  10,60               7622                                                                      /dev/binder
2   com.blues   2003  system  mem  unknown                                                            /dev/ashmem/dalvik-indirect ref table (deleted)
3   com.blues   2003  system  mem  unknown                            /dev/ashmem/dalvik-allocspace zygote / non moving space live-bitmap 0 (deleted)
4   com.blues   2003  system  mem      REG    8,1   8774704   263011                                                            /system/lib/libart.so
5   com.blues   2003  system  mem      REG    8,1     29176   263435                                               /system/fonts/NotoSansLao-Bold.ttf
6   com.blues   2003  system  mem      REG    8,1    411120   262703                                                   /system/lib/libinputflinger.so
7   com.andro  19725  u0_a54  cwd      DIR    0,2       820        2                                                                                /
8   com.andro  19725  u0_a54  rtd      DIR    0,2       820        2                                                                                /
9   com.andro  19725  u0_a54  txt      REG    8,1     17948   262260                                                        /system/bin/app_process32
10  com.andro  19725  u0_a54  mem  unknown                                                                    /dev/ashmem/dalvik-main space (deleted)
11  com.andro  19725  u0_a54  mem  unknown                                                                  /dev/ashmem/dalvik-main space 1 (deleted)
12  com.andro  19725  u0_a54  mem      REG   8,17   2125824  2228227                                 /data/dalvik-cache/x86/system@framework@boot.art
13  com.andro  19725  u0_a54  mem      REG   8,17   1167360  2228229                     /data/dalvik-cache/x86/system@framework@boot-core-libart.art
14  com.andro  19725  u0_a54  mem      REG    8,1      5142   263912                                         /system/usr/hyphen-data/hyph-mn-cyrl.hyb
15  com.andro  19725  u0_a54  mem      REG    8,1     35913   263879                                              /system/usr/hyphen-data/hyph-cy.hyb
16  com.andro  19725  u0_a54  mem  unknown                                                 /dev/ashmem/dalvik-large object space allocation (deleted)
17  com.andro  19725  u0_a54  mem      REG    8,1     67076   262937                                             /system/lib/libkeymaster_messages.so
18  com.andro  19725  u0_a54  mem      REG    8,1    202252   262648                                                     /system/lib/libkeymaster1.so
19  com.andro  19725  u0_a54  mem      REG    8,1    160904   262967                                            /system/lib/libsoftkeymasterdevice.so
20  com.andro  19725  u0_a54  mem      REG    8,1    156172   262657                                                     /system/lib/libjavacrypto.so
21  com.andro  19725  u0_a54  mem      REG    8,1    124456   263004                                                /system/lib/libkeystore_binder.so
22  com.andro  19725  u0_a54  mem  unknown                                                 /dev/ashmem/dalvik-large object space allocation (deleted)
23  com.andro  19725  u0_a54  mem  unknown                                                 /dev/ashmem/dalvik-large object space allocation (deleted)
24  com.andro  19725  u0_a54  mem  unknown                                                 /dev/ashmem/dalvik-large object space allocation (deleted)
25  com.andro  19725  u0_a54  mem      REG   0,15    131072     6346                                      /dev/__properties__/u:object_r:logd_prop:s0
26  com.andro  19725  u0_a54  mem      REG   0,15    131072     6339                                   /dev/__properties__/u:object_r:default_prop:s0
27  com.andro  19725  u0_a54  mem      REG    8,1      8165   263886                                              /system/usr/hyphen-data/hyph-fr.hyb
28  com.andro  19725  u0_a54  mem  unknown                                                 /dev/ashmem/dalvik-large object space allocation (deleted)
29  com.andro  19725  u0_a54  mem      REG    8,1       607   263890                                              /system/usr/hyphen-data/hyph-pa.hyb
30  com.andro  19725  u0_a54  mem      REG    8,1      9716   262949                                                /system/lib/libkeystore-engine.so
31  com.andro  19725  u0_a54  mem      REG    8,1       647   263924                                              /system/usr/hyphen-data/hyph-or.hyb
32  com.andro  19725  u0_a54  mem  unknown                                                 /dev/ashmem/dalvik-large object space allocation (deleted)
33  com.andro  19725  u0_a54  mem      REG    8,1    518036   262595                                                      /system/lib/libmedia_jni.so
34  com.andro  19725  u0_a54  mem      REG    8,1    202168   263023                                                           /system/lib/libexif.so
35  com.andro  19725  u0_a54  mem      REG    8,1    136632   262593                                                            /system/lib/libmtp.so
36  com.andro  19725  u0_a54  mem      REG    8,1     71116   263050                                       /system/lib/libstagefright_amrnb_common.so
37  com.andro  19725  u0_a54  mem      REG    8,1       687   263891                                              /system/usr/hyphen-data/hyph-mr.hyb
38  com.andro  19725  u0_a54  mem      REG   0,15    131072     6352                                       /dev/__properties__/u:object_r:log_prop:s0
39  com.andro  19725  u0_a54  mem  unknown                                                 /dev/ashmem/dalvik-large object space allocation (deleted)
40  com.andro  19725  u0_a54  mem      REG    8,1    504430   263754                                                /system/usr/share/zoneinfo/tzdata
41  com.andro  19725  u0_a54  mem      REG    8,1  18677700   263362                                            /system/fonts/NotoSansCJK-Regular.ttc
42  com.andro  19725  u0_a54  mem      REG    8,1      6967   263882                                              /system/usr/hyphen-data/hyph-da.hyb
43  com.andro  19725  u0_a54  mem  unknown                                                 /dev/ashmem/dalvik-large object space allocation (deleted)
44  com.andro  19725  u0_a54  mem  unknown                                                 /dev/ashmem/dalvik-large object space allocation (deleted)
45  com.andro  19725  u0_a54  mem      REG    8,1     40308   263449                                        /system/fonts/CarroisGothicSC-Regular.ttf
46  com.andro  19725  u0_a54  mem      REG    8,1  22201456   263865                                                     /system/usr/icu/icudt56l.dat
47  com.andro  19725  u0_a54  mem  unknown                                                                   /dev/ashmem/dalvik-LinearAlloc (deleted)
48  com.andro  19725  u0_a54  mem      REG   8,17   1663816  2228313      /data/dalvik-cache/x86/system@app@PrintSpooler@PrintSpooler.apk@classes.dex
49  com.andro  19725  u0_a54  mem  unknown                                                            /dev/ashmem/dalvik-indirect ref table (deleted)
50  com.andro  19725  u0_a54  mem  unknown                                                            /dev/ashmem/dalvik-indirect ref table (deleted)
51  com.andro  19725  u0_a54  mem      REG    8,1   4912800   262602                                                   /system/lib/libart-compiler.so
52  com.andro  19725  u0_a54  mem      REG    8,1   1232260   262969                                                           /system/lib/libvixl.so
53  com.andro  19725  u0_a54  mem      REG    8,1  22201456   263865                                                     /system/usr/icu/icudt56l.dat
54  com.andro  19725  u0_a54  mem  unknown                                               /dev/ashmem/dalvik-Jit thread pool worker thread 0 (deleted)
55  com.andro  19725  u0_a54  mem      CHR  10,60               7622                                                                      /dev/binder
56  com.andro  19725  u0_a54  mem  unknown                            /dev/ashmem/dalvik-allocspace zygote / non moving space live-bitmap 0 (deleted)
57  com.andro  19725  u0_a54  mem      REG    8,1   8774704   263011                                                            /system/lib/libart.so
58  com.andro  19725  u0_a54  mem      REG    8,1     29176   263435                                               /system/fonts/NotoSansLao-Bold.ttf
59  com.andro  19725  u0_a54  mem      REG    8,1    411120   262703                                                   /system/lib/libinputflinger.so
60  com.andro  19725  u0_a54  mem      REG    8,1     42532   262665                                                   /system/lib/libnativeloader.so
61  com.andro  19725  u0_a54  mem      REG    8,1     30228   262758                                                /system/lib/libhardware_legacy.so
62  com.andro  19725  u0_a54  mem      REG    8,1     46512   263059                                                             /system/lib/libRS.so


```
