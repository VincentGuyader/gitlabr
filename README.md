
<!-- README.md is generated from README.Rmd. Please edit that file -->

# {gitlabr}

<!-- badges: start -->

[![CRAN\_Status\_Badge](https://www.r-pkg.org/badges/version/gitlabr)](https://cran.r-project.org/package=gitlabr)
![CRAN Downloads Badge](https://cranlogs.r-pkg.org/badges/gitlabr) [![R
build
status](https://github.com/statnmap/gitlabr/workflows/R-CMD-check/badge.svg)](https://github.com/statnmap/gitlabr/actions)
<!-- badges: end -->

## Installation

You can install the most recent stable version from CRAN using:

``` r
install.packages("gitlabr")
```

To install the development version using
[devtools](https://cran.r-project.org/package=devtools), type:

``` r
devtools::install_github("statnmap/gitlabr")
```

See the [CONTRIBUTING.md](CONTRIBUTING.md) for instructions on how to
run tests locally and contributor information.

## Recommended GitLab versions

GitLab 11.6 or higher is generally recommended when using {gitlabr}
version 1.1.6 or higher. This {gitlabr} version uses the GitLab API v4.

## Quick Start Example

R code using {gitlabr} to perform some common GitLab actions can look
like this

  - Store your token in .Renviron with `usethis::edit_r_environ()` and
    restart your session

  - Set a connection to GitLab instance

<!-- end list -->

``` r
library(gitlabr)

# Add: GITLAB_COM_TOKEN=YourTokenHere
# You can verify it worked
# Sys.getenv("GITLAB_COM_TOKEN")

# connect as a fixed user to a gitlab instance
my_gitlab <- gl_connection(
  gitlab_url = "https://gitlab.com",
  private_token = Sys.getenv("GITLAB_COM_TOKEN"))
# a function is returned
# its first argument is the request (name or function), optionally followed by parameters

# Set the connection for the session
set_gitlab_connection(my_gitlab)
```

  - Find the list of projects available to you
      - Define a limit of pages of projects to search in with
        `max_page`, otherwise the entire GitLab.com will be downloaded
        here…

<!-- end list -->

``` r
# a tibble is returned, as is always by {gitlabr} functions
gl_list_projects(max_page = 2) 
#> # A tibble: 200 x 119
#>    id    description name  name_with_names… path  path_with_names… created_at
#>    <chr> <chr>       <chr> <chr>            <chr> <chr>            <chr>     
#>  1 2169… "A calenda… preg… mister ragondin… preg… ragondin/pregna… 2020-10-1…
#>  2 2169… "Vue - Com… vue-… Rogério de Oliv… vue-… RogerMitoProjec… 2020-10-1…
#>  3 2169… "Generate … live… Jacob Shodd / l… live… jshodd/live-bui… 2020-10-1…
#>  4 2169… "PPW story… stor… ahmad harori / … stor… ahmadharorizaki… 2020-10-1…
#>  5 2169… ""          Home… dara lon / Home… home… MrDara/homework… 2020-10-1…
#>  6 2169… ""          Data  Jan Škařupa / D… data  skarupa/data     2020-10-1…
#>  7 2169… "Detection… MSI-… sameerimamillap… msi-… sameerimamillap… 2020-10-1…
#>  8 2169…  <NA>       sara… sarahfiola / sa… sara… sarahfiolaa/sar… 2020-10-1…
#>  9 2169… ""          ar m… By Gvz / ar muse ar-m… bygvz123/ar-muse 2020-10-1…
#> 10 2169… ""          stc_… Roman Akhmaduli… stc_… Roman_Akhmaduli… 2020-10-1…
#> # … with 190 more rows, and 112 more variables: ssh_url_to_repo <chr>,
#> #   http_url_to_repo <chr>, web_url <chr>, forks_count <chr>, star_count <chr>,
#> #   last_activity_at <chr>, namespace.id <chr>, namespace.name <chr>,
#> #   namespace.path <chr>, namespace.kind <chr>, namespace.full_path <chr>,
#> #   namespace.avatar_url <chr>, namespace.web_url <chr>, `_links.self` <chr>,
#> #   `_links.issues` <chr>, `_links.merge_requests` <chr>,
#> #   `_links.repo_branches` <chr>, `_links.labels` <chr>, `_links.events` <chr>,
#> #   `_links.members` <chr>, packages_enabled <chr>, empty_repo <chr>,
#> #   archived <chr>, visibility <chr>, owner.id <chr>, owner.name <chr>,
#> #   owner.username <chr>, owner.state <chr>, owner.avatar_url <chr>,
#> #   owner.web_url <chr>, resolve_outdated_diff_discussions <chr>,
#> #   container_registry_enabled <chr>,
#> #   container_expiration_policy.cadence <chr>,
#> #   container_expiration_policy.enabled <chr>,
#> #   container_expiration_policy.keep_n <chr>,
#> #   container_expiration_policy.older_than <chr>,
#> #   container_expiration_policy.next_run_at <chr>, issues_enabled <chr>,
#> #   merge_requests_enabled <chr>, wiki_enabled <chr>, jobs_enabled <chr>,
#> #   snippets_enabled <chr>, service_desk_enabled <chr>,
#> #   service_desk_address <chr>, can_create_merge_request_in <chr>,
#> #   issues_access_level <chr>, repository_access_level <chr>,
#> #   merge_requests_access_level <chr>, forking_access_level <chr>,
#> #   wiki_access_level <chr>, builds_access_level <chr>,
#> #   snippets_access_level <chr>, pages_access_level <chr>,
#> #   shared_runners_enabled <chr>, lfs_enabled <chr>, creator_id <chr>,
#> #   import_status <chr>, open_issues_count <chr>, ci_default_git_depth <chr>,
#> #   public_jobs <chr>, build_timeout <chr>,
#> #   auto_cancel_pending_pipelines <chr>, ci_config_path <chr>,
#> #   only_allow_merge_if_pipeline_succeeds <chr>, request_access_enabled <chr>,
#> #   only_allow_merge_if_all_discussions_are_resolved <chr>,
#> #   remove_source_branch_after_merge <chr>,
#> #   printing_merge_request_link_enabled <chr>, merge_method <chr>,
#> #   auto_devops_enabled <chr>, auto_devops_deploy_strategy <chr>,
#> #   autoclose_referenced_issues <chr>, approvals_before_merge <chr>,
#> #   mirror <chr>, external_authorization_classification_label <chr>,
#> #   default_branch <chr>, readme_url <chr>, forked_from_project.id <chr>,
#> #   forked_from_project.description <chr>, forked_from_project.name <chr>,
#> #   forked_from_project.name_with_namespace <chr>,
#> #   forked_from_project.path <chr>,
#> #   forked_from_project.path_with_namespace <chr>,
#> #   forked_from_project.created_at <chr>,
#> #   forked_from_project.default_branch <chr>,
#> #   forked_from_project.ssh_url_to_repo <chr>,
#> #   forked_from_project.http_url_to_repo <chr>,
#> #   forked_from_project.web_url <chr>, forked_from_project.readme_url <chr>,
#> #   forked_from_project.forks_count <chr>,
#> #   forked_from_project.star_count <chr>,
#> #   forked_from_project.last_activity_at <chr>,
#> #   forked_from_project.namespace.id <chr>,
#> #   forked_from_project.namespace.name <chr>,
#> #   forked_from_project.namespace.path <chr>,
#> #   forked_from_project.namespace.kind <chr>,
#> #   forked_from_project.namespace.full_path <chr>,
#> #   forked_from_project.namespace.parent_id <chr>,
#> #   forked_from_project.namespace.avatar_url <chr>,
#> #   forked_from_project.namespace.web_url <chr>, …
```

  - Explore one of your projects. You can set the name of the project or
    its ID. The ID is highly recommended, in particular if your project
    does not appear in the first pages of projects above.
      - Let’s explore [project
        “repo.rtask”](https://gitlab.com/statnmap/repo.rtask), with
        `ID = 20384533` on GitLab.com

<!-- end list -->

``` r
my_project <- 20384533 #repo.rtask",
```

  - List files of the project using `gl_list_files`

<!-- end list -->

``` r
gl_list_files(project = my_project)
#> # A tibble: 2 x 5
#>   id                                       name        type  path        mode  
#>   <chr>                                    <chr>       <chr> <chr>       <chr> 
#> 1 9c66eff9a1f6f34b6d9108ef07d76f8ce4c4e47f NEWS.md     blob  NEWS.md     100644
#> 2 c36b681bb31b80cbd090f07c95f09788c88629a6 example.txt blob  example.txt 100644
```

  - List issues with `gl_list_issues`

<!-- end list -->

``` r
gl_list_issues(project = my_project)
#> # A tibble: 12 x 51
#>    id    iid   project_id title state created_at updated_at closed_at
#>    <chr> <chr> <chr>      <chr> <chr> <chr>      <chr>      <chr>    
#>  1 7249… 12    20384533   Impl… clos… 2020-10-1… 2020-10-1… 2020-10-…
#>  2 7249… 11    20384533   Impl… clos… 2020-10-1… 2020-10-1… 2020-10-…
#>  3 7249… 10    20384533   Impl… clos… 2020-10-1… 2020-10-1… 2020-10-…
#>  4 7249… 9     20384533   Impl… clos… 2020-10-1… 2020-10-1… 2020-10-…
#>  5 7249… 8     20384533   Impl… clos… 2020-10-1… 2020-10-1… 2020-10-…
#>  6 7249… 7     20384533   Impl… clos… 2020-10-1… 2020-10-1… 2020-10-…
#>  7 7186… 6     20384533   Impl… clos… 2020-09-2… 2020-09-2… 2020-09-…
#>  8 6972… 5     20384533   Impl… clos… 2020-08-1… 2020-08-1… 2020-08-…
#>  9 6972… 4     20384533   Impl… clos… 2020-08-1… 2020-08-1… 2020-08-…
#> 10 6972… 3     20384533   Impl… clos… 2020-08-1… 2020-08-1… 2020-08-…
#> 11 6952… 2     20384533   A se… open… 2020-08-0… 2020-08-0… <NA>     
#> 12 6952… 1     20384533   An e… open… 2020-08-0… 2020-08-0… <NA>     
#> # … with 43 more variables: closed_by.id <chr>, closed_by.name <chr>,
#> #   closed_by.username <chr>, closed_by.state <chr>,
#> #   closed_by.avatar_url <chr>, closed_by.web_url <chr>, assignees.id <chr>,
#> #   assignees.name <chr>, assignees.username <chr>, assignees.state <chr>,
#> #   assignees.avatar_url <chr>, assignees.web_url <chr>, author.id <chr>,
#> #   author.name <chr>, author.username <chr>, author.state <chr>,
#> #   author.avatar_url <chr>, author.web_url <chr>, assignee.id <chr>,
#> #   assignee.name <chr>, assignee.username <chr>, assignee.state <chr>,
#> #   assignee.avatar_url <chr>, assignee.web_url <chr>, user_notes_count <chr>,
#> #   merge_requests_count <chr>, upvotes <chr>, downvotes <chr>,
#> #   confidential <chr>, web_url <chr>, time_stats.time_estimate <chr>,
#> #   time_stats.total_time_spent <chr>, task_completion_status.count <chr>,
#> #   task_completion_status.completed_count <chr>, has_tasks <chr>,
#> #   `_links.self` <chr>, `_links.notes` <chr>, `_links.award_emoji` <chr>,
#> #   `_links.project` <chr>, references.short <chr>, references.relative <chr>,
#> #   references.full <chr>, description <chr>
```

  - Create an issue

<!-- end list -->

``` r
# create a new issue
new_feature_issue <- gl_new_issue(title = "Implement new feature", project = my_project)

# statnmap user ID
my_id <- 4809823

# assign issue to me
gl_assign_issue(new_feature_issue$iid,
                assignee_id = my_id,
                project = my_project)
#> # A tibble: 1 x 44
#>   id    iid   project_id title state created_at updated_at assignees.id
#>   <chr> <chr> <chr>      <chr> <chr> <chr>      <chr>      <chr>       
#> 1 7249… 13    20384533   Impl… open… 2020-10-1… 2020-10-1… 4809823     
#> # … with 36 more variables: assignees.name <chr>, assignees.username <chr>,
#> #   assignees.state <chr>, assignees.avatar_url <chr>, assignees.web_url <chr>,
#> #   author.id <chr>, author.name <chr>, author.username <chr>,
#> #   author.state <chr>, author.avatar_url <chr>, author.web_url <chr>,
#> #   assignee.id <chr>, assignee.name <chr>, assignee.username <chr>,
#> #   assignee.state <chr>, assignee.avatar_url <chr>, assignee.web_url <chr>,
#> #   user_notes_count <chr>, merge_requests_count <chr>, upvotes <chr>,
#> #   downvotes <chr>, confidential <chr>, web_url <chr>,
#> #   time_stats.time_estimate <chr>, time_stats.total_time_spent <chr>,
#> #   task_completion_status.count <chr>,
#> #   task_completion_status.completed_count <chr>, has_tasks <chr>,
#> #   `_links.self` <chr>, `_links.notes` <chr>, `_links.award_emoji` <chr>,
#> #   `_links.project` <chr>, references.short <chr>, references.relative <chr>,
#> #   references.full <chr>, subscribed <chr>

# Verify new issue is here
gl_list_issues(state = "opened", my_project)
#> # A tibble: 3 x 44
#>   id    iid   project_id title state created_at updated_at assignees.id
#>   <chr> <chr> <chr>      <chr> <chr> <chr>      <chr>      <chr>       
#> 1 7249… 13    20384533   Impl… open… 2020-10-1… 2020-10-1… 4809823     
#> 2 6952… 2     20384533   A se… open… 2020-08-0… 2020-08-0… <NA>        
#> 3 6952… 1     20384533   An e… open… 2020-08-0… 2020-08-0… <NA>        
#> # … with 36 more variables: assignees.name <chr>, assignees.username <chr>,
#> #   assignees.state <chr>, assignees.avatar_url <chr>, assignees.web_url <chr>,
#> #   author.id <chr>, author.name <chr>, author.username <chr>,
#> #   author.state <chr>, author.avatar_url <chr>, author.web_url <chr>,
#> #   assignee.id <chr>, assignee.name <chr>, assignee.username <chr>,
#> #   assignee.state <chr>, assignee.avatar_url <chr>, assignee.web_url <chr>,
#> #   user_notes_count <chr>, merge_requests_count <chr>, upvotes <chr>,
#> #   downvotes <chr>, confidential <chr>, web_url <chr>,
#> #   time_stats.time_estimate <chr>, time_stats.total_time_spent <chr>,
#> #   task_completion_status.count <chr>,
#> #   task_completion_status.completed_count <chr>, has_tasks <chr>,
#> #   `_links.self` <chr>, `_links.notes` <chr>, `_links.award_emoji` <chr>,
#> #   `_links.project` <chr>, references.short <chr>, references.relative <chr>,
#> #   references.full <chr>, description <chr>

# close issue
gl_close_issue(new_feature_issue$iid, project = my_project)$state
#> [1] "closed"
```

## Further information

  - For a comprehensive overview & introduction see the
    `vignette("quick-start-guide-to-gitlabr")`
  - When writing custom extensions (“convenience functions”) for
    {gitlabr} or when you experience any trouble, the very extensive
    [GitLab API documentation](http://doc.gitlab.com/ce/api/) can be
    helpful.

*Note that the {gitlabr} package was originally created by [Jirka
Lewandowski](https://github.com/jirkalewandowski/gitlabr). The present
repository is a fork to be able to continue development of this
package.*

# Contributing to {gitlabr}

You’re welcome to contribute to {gitlabr} by editing the source code,
adding more convenience functions, filing issues, etc.
[CONTRIBUTING.md](CONTRIBUTING.md) compiles some information helpful in
that process.

Please also note the [Code of Conduct](CONDUCT.md).
