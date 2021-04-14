# 账号中心：用户设置调用规则

##### 上传设置信息

1. 上传单个设置信息

```java
/**
     *
     * 上传用户设置信息
     * 单个设置----用户个性化设置
     */
    public void onSetSingle(View v){

        PersonalizationInfo personalizationInfo = new PersonalizationInfo();

        //  ModuleType 为你当前所处模块的ModuleType
        // 必传字段
        personalizationInfo.setModule(ModuleType.SETTING+"");


        // 你需要设置的设置项
        //（项自定义）比如 音量:volumn volumn1  亮度:light  light1  空调开关：airSwitch
        //必传字段
        personalizationInfo.setItem("volumn100");

        // 设置项对应的值
        //必传字段
        personalizationInfo.setValue("341");


        // 1 代表用户设置（跟随账号）  2代表车机设置（跟随车机）
        // 必传
        personalizationInfo.setType(1);


        // 调用bnuxApi的方法进行设置
        AccountProxy.getInstance().setDataSync(personalizationInfo);

    }
```



2. 批量上传设置信息

   ```java
   /**
        *
        * 上传用户设置信息
        * 批量设置----用户个性化设置
        */
       public void onSetMulti(View v){
           ArrayList<PersonalizationInfo> list = new ArrayList<>();
           for (int i = 0;i<3;i++){
               PersonalizationInfo personalizationInfo = new PersonalizationInfo();
   
               //  ModuleType 为你当前所处模块的ModuleType
               // 必传字段
               personalizationInfo.setModule(ModuleType.SETTING+"");
   
               // 你需要设置的设置项
               //（项自定义）比如 音量:volumn volumn1  亮度:light  light1  空调开关：airSwitch
               //必传字段
               personalizationInfo.setItem("volumn1"+i);
   
               // 1 代表用户设置（跟随账号）  2代表车机设置（跟随车机）
               personalizationInfo.setType(1);
   
               // 设置项对应的值
               //必传字段
               personalizationInfo.setValue(""+i);
   
               list.add(personalizationInfo);
           }
           // 调用bnuxApi的方法进行设置
           AccountProxy.getInstance().setAllDataSync(list);
   
       }
   ```

   

##### 获取设置信息

​    如果需要主动获取用户设置信息，则按下面方法调用

```
 /**
     *
     * 获取信息
     * 获取数据-----用户个性化设置
     */
    public void onGet(View v){
        // ModuleType 为你当前所处模块的ModuleType
        // 必传字段
        ArrayList<PersonalizationInfo> list = AccountProxy.getInstance().getAllDataSync(ModuleType.SETTING+"");
        if(list == null){
            return;
        }

        for (int i = 0 ;i<list.size();i++){
            BnLogHelper.LogD(list.get(i).getItem()+":"+list.get(i).getValue());
        }
    }
```

##### 异步消息监听

-  用户中心会在以下情况下去云端获取用户设置数据
  1. 开机，做用户数据同步
  2. 账号切换时，做用户数据同步

- 如有接受用户数据同步消息需求，则需监听异步消息

  ```
  package com.bqaccount.user_setting_demo;
  
  import android.os.Bundle;
  
  import com.bnux.api.bus.async.OctoBusEvent;
  import com.bnux.api.bus.async.OctoBusProxy;
  import com.bnux.api.bus.type.ModuleType;
  import com.bnux.api.common.tools.log.BnLogHelper;
  import com.bnux.api.module.account.AccountEvent;
  import com.bnux.api.module.account.AccountKey;
  import com.bnux.api.module.account.bean.PersonalizationInfo;
  
  import java.util.ArrayList;
  
  /**
   * Copyright (C), 2017-2021, 宝能有限公司
   * Author: jayce.feng
   * Date: 2021/4/12
   * Description: 监听账号模块异步发出的用户设置刷新消息
   * 1. 账号服务会在开机时刷新用户数据
   * 2，账号模块会在切换账号时刷新用户数据
   * 3. 账号模块会在获取到服务器数据时，发出一个全局异步消息，通知各模块去刷新用户相关的设置数据
   * version v1.0
   */
  public class DemoOctoBusListener implements com.bnux.api.bus.async.OctoBusListener {
      private static DemoOctoBusListener listener;
  
      private DemoOctoBusListener(){
  
      }
  
      public static  DemoOctoBusListener getInstance(){
          if(listener == null){
              synchronized (DemoOctoBusListener.class){
                  if(listener == null){
                      listener = new DemoOctoBusListener();
                  }
              }
          }
          return listener;
      }
  
  
      public void init(){
          OctoBusProxy.getInstance().registerOctoBusListener(this);
          OctoBusProxy.getInstance().subscribe(new OctoBusEvent(ModuleType.ACCOUNT,AccountEvent.NOTIFY_DATA_SYNC_ALL));
  
      }
  
      @Override
      public void onOctoBusCallBack(OctoBusEvent event) {
          Bundle bundle  = event.getBundle();
          if(bundle == null){
              return;
          }
          bundle.setClassLoader(getClass().getClassLoader());
          switch (event.getEventName()){
              case AccountEvent.NOTIFY_DATA_SYNC_ALL:
                 ArrayList<PersonalizationInfo> list =  bundle.getParcelableArrayList(AccountKey.DATA);
                 if(list == null){
                     break;
                 }
                  for (int i = 0; i <list.size() ; i++) {
                      BnLogHelper.LogD(list.get(i).getItem()+"---"+list.get(i).getValue());
  
                  }
                  break;
              default:
                  break;
          }
      }
  }
  
  ```

  