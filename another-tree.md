Here's the detailed folder structure for your CodeIgniter HMVC application with the `admin` and `user` modules, including the specific controllers you mentioned (`category`, `blog`, `post` for admin, and `profile`, `account`, `subscription` for user):

```
application/
├── core/
│   └── MY_Controller.php
├── modules/
│   ├── admin/
│   │   ├── controllers/
│   │   │   ├── Admin.php             # Main admin controller
│   │   │   ├── Category.php         # Category management
│   │   │   ├── Blog.php             # Blog management
│   │   │   └── Post.php             # Post management
│   │   ├── models/
│   │   │   ├── Category_model.php
│   │   │   ├── Blog_model.php
│   │   │   └── Post_model.php
│   │   └── views/
│   │       ├── category/
│   │       │   ├── index.php
│   │       │   ├── create.php
│   │       │   └── edit.php
│   │       ├── blog/
│   │       │   ├── index.php
│   │       │   ├── create.php
│   │       │   └── edit.php
│   │       └── post/
│   │           ├── index.php
│   │           ├── create.php
│   │           └── edit.php
│   │
│   └── user/
│       ├── controllers/
│       │   ├── User.php             # Main user controller
│       │   ├── Profile.php          # User profile
│       │   ├── Account.php          # Account settings
│       │   └── Subscription.php     # Subscription management
│       ├── models/
│       │   ├── Profile_model.php
│       │   ├── Account_model.php
│       │   └── Subscription_model.php
│       └── views/
│           ├── profile/
│           │   ├── index.php
│           │   └── edit.php
│           ├── account/
│           │   ├── index.php
│           │   └── security.php
│           └── subscription/
│               ├── index.php
│               ├── plans.php
│               └── payment.php
└── ...
```

## Example Controller Structure

**Admin/Category.php** (application/modules/admin/controllers/Category.php):
```php
<?php
defined('BASEPATH') OR exit('No direct script access allowed');

class Category extends Admin_Controller {
    public function __construct() {
        parent::__construct();
        $this->load->model('category_model');
    }

    public function index() {
        $data['categories'] = $this->category_model->get_all();
        $this->load->view('admin/category/index', $data);
    }

    public function create() {
        // Create category logic
        $this->load->view('admin/category/create');
    }
}
```

**User/Profile.php** (application/modules/user/controllers/Profile.php):
```php
<?php
defined('BASEPATH') OR exit('No direct script access allowed');

class Profile extends User_Controller {
    public function __construct() {
        parent::__construct();
        $this->load->model('profile_model');
    }

    public function index() {
        $data['profile'] = $this->profile_model->get_user_profile($this->user_id);
        $this->load->view('user/profile/index', $data);
    }

    public function edit() {
        // Edit profile logic
        $this->load->view('user/profile/edit');
    }
}
```

## Base Controllers

It's recommended to create base controllers for each module:

1. **Admin_Controller.php** (application/core/Admin_Controller.php):
```php
<?php
defined('BASEPATH') OR exit('No direct script access allowed');

class Admin_Controller extends MY_Controller {
    public function __construct() {
        parent::__construct();
        // Check admin authentication
        // Load admin assets
    }
}
```

2. **User_Controller.php** (application/core/User_Controller.php):
```php
<?php
defined('BASEPATH') OR exit('No direct script access allowed');

class User_Controller extends MY_Controller {
    public function __construct() {
        parent::__construct();
        // Check user authentication
        // Load user assets
    }
}
```

This structure provides:
1. Clear separation between admin and user functionality
2. Logical grouping of related features
3. Consistent naming conventions
4. Easy maintenance and scalability
5. Proper organization of views in subfolders matching their controllers
