## Ansible 赋能
红帽(Red hat)如何做自动化

---

#### 基本概念
- Inventory 环境管理
- Task 模块化任务
- Env 环境变量
- Var 传参
- Playbook = task+env+var+inventory

---

#### Task Example1 - Shell

```yml
- name: get kube-apiserver pods
  ansible.builtin.shell
	kubectl get pod -n fst-manage | grep kube-apiserver | awk '{print $1}'
```

---

#### Task Example2 - Copy

```yml
- name: upload images
  ansible.builtin.copy
    src: kube-prometheus.tar.gz
    dest: /opt/templates/
```

---

#### Inventory

![[Pasted image 20230328224258.png]]

---

#### Inventory配置技巧
- all:vars设置inventory中全部主机
- 根据不同密码组合来分组
- 同一个host可以有多个分组

---

#### 项目初始化

---

#### 初始化ansible role
```
mkdir roles
ansible-galaxy init roles/prometheus
```

---

#### role项目目录
   ```
   <role_name>/
   ├── README.md
   ├── defaults 默认值
   │   └── main.yml
   ├── files 待上传文件/下载文件
   ├── handlers 回调
   │   └── main.yml
   ├── meta 元数据
   │   └── main.yml
   ├── tasks 任务
   │   └── main.yml
   ├── templates jinja2模板
   ├── tests 测试用例
   │   ├── inventory
   │   └── test.yml
   └── vars 变量
       └── main.yml
   ```

---

#### 使用role
```yml
# playbook首行应添加---, 当前为规避advanced slide插件因此去掉了
- name: use prometheus role playbook
  hosts: node2
  roles:
    - prometheus
```

---

## 现场演示

如何用ansible自动化部署Prometheus

---

#### 重点
- handler+幂等性 - 避免重复上传镜像
- ansible + shell/python
- jsonnet 自定义配置

---

|          | ansible | shell |
| -------- | ------- | ----- |
| 抽象层次 | 高      | 低    |
| 可移植性 | 强      | 弱    |
| 易用性   | 强      | 弱    |
| 可读性   | 强      | 弱    |
| 约束     | 强      | 弱    |

---

#### Future
- 静态pod换包
- 清理I层资源
- 日志采集/分析
- 配置wsl执行机
- ... 全部一行命令完成!


---

备忘

---

使用jinja2 template
```yml
- name: template vhost file
  template:
    src: vhost.conf.j2
    dest: /etc/httpd/conf.d/vhost.conf
    owner: root
    group: root
    mode: 0644
  notify:
    - restart_httpd
```

---

杂
- `/etc/motd` 在ssh登入时展示的内容
- 自定义module: swrctl模块, 查到有镜像则不上传
- ansible-navigator
- ansible-galaxy
- 标准的目录结构
- 通过http下载 `ansible-doc ansible.builtin.get_url`


