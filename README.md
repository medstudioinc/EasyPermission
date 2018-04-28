# EasyPermission

A Library which will help you to easily ask all permission without writing a lot of codes.

![](https://github.com/sachinvarma/EasyPermission/blob/master/Art/demo.gif)

**Why this ?**

1)It will automatically check whether the permission is granted or not.

2)If permission is granted -> No action else Permission will be asked.

3)Can ask multiple permission easily.

4)Denied Permission list will be provided.

**How to Add :**

Via Gradle:

```
repositories {
        maven { url "https://jitpack.io" }
    }
```
```
implementation 'com.github.sachinvarma:EasyPermission:1.0.0'
```

Via Maven:

```
<dependency>
 <groupId>com.github.sachinvarma</groupId>
 <artifactId>EasyPermission</artifactId>
 <version>1.0.0</version>
</dependency> 
```

**How it works:**

1) Create a List of Permissions you want to ask,

```
 List<String> permission = new ArrayList<>();
 permission.add(EasyPermissionList.READ_EXTERNAL_STORAGE);
 permission.add(EasyPermissionList.ACCESS_FINE_LOCATION);
```
2) Call EasyPermissionInit,

```
 new EasyPermissionInit(MainActivity.this, permission);
``` 
That's all

3) Response will be received in onActivityResult()

```
@Override
  protected void onActivityResult(int requestCode, int resultCode, Intent data) {
    super.onActivityResult(requestCode, resultCode, data);

    switch (requestCode) {
      case EasyPermissionConstants.INTENT_CODE:

        if (data != null) {
          boolean isGotAllPermissions =
            data.getBooleanExtra(EasyPermissionConstants.IS_GOT_ALL_PERMISSION, false);

          if(data.hasExtra(EasyPermissionConstants.IS_GOT_ALL_PERMISSION)){
          if (isGotAllPermissions) {
            Toast.makeText(this, "All Permissions Granted", Toast.LENGTH_SHORT).show();
          } else {
            Toast.makeText(this, "All permission not Granted", Toast.LENGTH_SHORT).show();
          }}

          // if you want to know which are the denied permissions.
          if (data.getSerializableExtra(EasyPermissionConstants.DENIED_PERMISSION_LIST) != null) {

            deniedPermissions = new ArrayList<>();

            deniedPermissions.addAll((Collection<? extends String>) data.getSerializableExtra(
              EasyPermissionConstants.DENIED_PERMISSION_LIST));

            if (deniedPermissions.size() > 0) {
              for (int i = 0; i < deniedPermissions.size(); i++) {
                switch (deniedPermissions.get(i)) {

                  case EasyPermissionList.READ_EXTERNAL_STORAGE:

                    Toast.makeText(this, "Storage Permission not granted", Toast.LENGTH_SHORT)
                      .show();

                    break;

                  case EasyPermissionList.ACCESS_FINE_LOCATION:

                    Toast.makeText(this, "Location Permission not granted", Toast.LENGTH_SHORT)
                      .show();

                    break;
                }
              }
            }
          }
        }
    }
  }
  ```
  
  For more Details - > 

https://github.com/sachinvarma/EasyPermission/blob/master/app/src/main/java/com/sachinvarma/easypermissionsample/MainActivity.java

**LICENSE**
```
Copyright (C) 2018 Sachin Varma

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

   http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.

```
