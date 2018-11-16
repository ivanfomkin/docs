# Перенести виртуальную машину в другую зону доступности

[!INCLUDE [instance-az](../../_includes_service/instance-az.md)]

Чтобы изменить зону доступность виртуальной машины:

1. Создайте снимок каждого из дисков виртуальной машины, см. раздел [[!TITLE]](../disk-control/create-snapshot.md).
1. Создайте виртуальную машину в другой зоне доступности с дисками из снимков, см. раздел [[!TITLE]](../vm-create/create-from-snapshots.md).
1. Удалите исходную виртуальную машину, см. раздел [[!TITLE]](vm-delete.md).