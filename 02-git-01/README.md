# Hello World

Описания файлов, которые будут проигнорированы:

 - ***/.terraform/* - скрытые директории terraform, не зависимо от того, на каком уровне вложенности находится папка terraform
 - **.tfstate* - файлы с расширением tfstate
 - **.tfstate.* - файлы с расширением tfstate после которых есть любые другие расширения
 - файлы crash.log, override.tf, override.tf.json, *_override.tf, *_override.tf.json
 - файлы с расширением *.tfvars
 - файлы .terraformrc и terraform.rc
