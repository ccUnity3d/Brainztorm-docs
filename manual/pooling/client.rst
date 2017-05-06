#################
Pooling Unity SDK
#################

`API Reference`_

**********
How to use
**********
For using this module, first you need activate it in `Brainztorm Settings Menu`_. 
After, in your code you can access the static members through the provided class 
:code:`Brainztorm.Pooling`.

.. note::

    For debugging purposes, it's recommended you activate the Pooling Log in the core 
    module Logging, through the `Brainztorm Settings Menu`_.

Using Pooling API
=================
:code:`Brainztorm.Pooling` provide the following members to interact with the module:

Properties:

- :code:`Logger`: read-only property that returns the own logger object for this module.

Methods:

- :code:`Prepare`: allocate an amount of object clones in the pool.
- :code:`GetAvailablePullObject`: pull an object instance from pool.
- :code:`Collect`: destroy unused objects from pool.
- :code:`Stats`: shows statistics in the Unity console about pooling use.
- :code:`DestroyPool`: destroy all objects and reset the pool.
- :code:`Resize`: changes the pool size.

The following code shows a useful application of Pooling: a gun behaviour. First, 
N(10 in the example) "bullet" objects are assigned in the pool and each shot will 
take a bullet from pool, after, the bullet object is deactivated and become 
available for future uses.

.. code-block:: c#

    using UnityEngine;
    using BzPooling = Brainztorm.Pooling;

    public class GunWithPooling : MonoBehaviour 
    {
        [SerializeField]
        private GameObject bullet;

        [SerializeField]
        private Transform bulletRoot;

        [SerializeField]
        private int initialPoolSize = 10;

        [SerializeField]
        private float fireRate = 0.2f;

        [SerializeField]
        private float strenght = 0.2f;

        private float elapsed;

        private void Awake()
        {
            Input.simulateMouseWithTouches = true;
        }

        private void Start()
        {
            BzPooling.Prepare(bullet, initialPoolSize, bulletRoot);
        }

        private void Update()
        {
            if (elapsed < fireRate)
                elapsed += Time.deltaTime;

            if (elapsed >= fireRate && Input.GetMouseButton(0))
                ShootFrom(Input.mousePosition);
        }

        private void ShootFrom(Vector3 screenPos)
        {
            elapsed = 0f;
            Ray ray = Camera.main.ScreenPointToRay(screenPos);

            GameObject instance = BzPooling.GetAvailablePullObject(prefab);
            instance.transform.position = ray.origin;
            instance.SetActive(true);
            instance.GetComponent<Rigidbody>().AddForce(ray.direction * strenght, ForceMode.Impulse);
        }
    }

.. _API Reference: #
.. _Brainztorm Settings Menu: #