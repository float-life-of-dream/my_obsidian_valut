如想使用哈希表运算, 您可以使用 uthash。 "uthash.h"已经默认被导入。请看如下示例:

1. 往哈希表中添加一个对象：

```c
struct hash_entry {
    int id;            /* we'll use this field as the key */
    char name[10];
    UT_hash_handle hh; /* makes this structure hashable */
};
struct hash_entry *users = NULL;

void add_user(struct hash_entry *s) {
    HASH_ADD_INT(users, id, s);
}
```

2. 在哈希表中查找一个对象：

```c
struct hash_entry *find_user(int user_id) {
    struct hash_entry *s;
    HASH_FIND_INT(users, &user_id, s);
    return s;
}
```

3. 从哈希表中删除一个对象：

```c
void delete_user(struct hash_entry *user) {
    HASH_DEL(users, user);  
}
```

