# memcached-operator with ansible

# Prerequisite

https://sdk.operatorframework.io/docs/building-operators/ansible/installation/

1. Docker
1. Python
1. `pip install ansible`
1. `pip install "ansible-runner<2.0"` <- Important https://github.com/operator-framework/operator-sdk/issues/5043
1. `pip install openshift`

# Steps to develop

1. Initialize operator with `ansible`

    ```
    operator-sdk init --domain example.com --plugins ansible
    ```

1. Create API resource

    ```
    operator-sdk create api --group cache --version v1alpha1 --kind Memcached --generate-role
    ```

1. Update `roles/memcached/tasks/main.yml`
1. Update `config/samples/cache_v1alpha1_memcached.yaml`

# Run locally outside the cluster

1. Run operator

    ```
    make install run
    ```

1. Apply CR

    ```
    kubectl apply -f config/samples/cache_v1alpha1_memcached.yaml
    ```

1. Check Deployment created by the operator

    ```
    kubectl get deployment
    NAME                         READY   UP-TO-DATE   AVAILABLE   AGE
    memcached-sample-memcached   3/3     3            3           6m28s
    ```

# Reference

https://sdk.operatorframework.io/docs/building-operators/ansible/tutorial/
