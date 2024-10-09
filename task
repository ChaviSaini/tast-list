
<?php


// Register activation hook to create options in the database
register_activation_hook(__FILE__, 'task_list_activate');

function task_list_activate() {
    add_option('task_list', []);
}

// Add admin menu
add_action('admin_menu', 'task_list_menu');

function task_list_menu() {
    add_menu_page('Task List', 'Task List', 'manage_options', 'task-list', 'task_list_page');
}

// Task list page
function task_list_page() {
    // Check if a task deletion request was made
    if (isset($_POST['delete_task'])) {
        $task_key = sanitize_text_field($_POST['delete_task']);
        $tasks = get_option('task_list');

        if (isset($tasks[$task_key])) {
            unset($tasks[$task_key]);
            update_option('task_list', $tasks);
            echo '<div class="notice notice-success"><p>Task deleted successfully!</p></div>';
        }
    }

  
    $tasks = get_option('task_list');
    ?>
    <div class="wrap">
        <h1>Task List</h1>
        <form method="post">
            <input type="text" name="new_task" placeholder="Add a new task" required>
            <input type="submit" value="Add Task">
        </form>
        <ul>
            <?php if (!empty($tasks)): ?>
                <?php foreach ($tasks as $key => $task): ?>
                    <li><?php echo esc_html($task); ?>
                        <form method="post" style="display:inline;">
                            <input type="hidden" name="delete_task" value="<?php echo esc_attr($key); ?>">
                            <button type="submit">Delete</button>
                        </form>
                    </li>
                <?php endforeach; ?>
            <?php endif; ?>
        </ul>
    </div>
    <?php
}

// Handle adding new tasks
add_action('init', 'handle_new_task');

function handle_new_task() {
    if (isset($_POST['new_task'])) {
        $tasks = get_option('task_list');
        $tasks[] = sanitize_text_field($_POST['new_task']);
        update_option('task_list', $tasks);
    }
}
?>
