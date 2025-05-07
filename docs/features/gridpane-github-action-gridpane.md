# GridPane GitHub Action | GridPane

# GridPane GitHub Action

 

1 min read 

 

### Information

This is NOT needed or necessary to understand or use our Git integration.

The following GitHub action was created by one of our developers. For those of you who know what it is and how to use it, we hope it will be helpful.

This is provided here as is, with no official GridPane support. If you need assistance with it, please only post in the community forum.

 

```
name: Push site to GridPane

on: push

jobs:
  sftp:

    runs-on: ubuntu-latest
    environment: main

    steps:
      - name: Checkout Repository
        uses: actions/checkout@v2
      - name: Rsync Deployment
        uses: Burnett01/rsync-deployments@5.2
        with:
          switches: -vrog --delete --chown=${{ secrets.GP_USER }}:${{ secrets.GP_USER }}
          path: ./
          remote_path: /home/${{ secrets.GP_USER }}/sites/${{ secrets.GP_SITE_URL }}/htdocs
          remote_host: ${{ secrets.GP_HOST }}
          remote_port: ${{ secrets.GP_HOST_PORT }}
          remote_user: root
          remote_key: ${{ secrets.GP_DEPLOY_KEY }}
```

 

#### Search the Knowledge Base

Search ...

 Results

See all results

#### New to GridPane?

Get started with our FREE Core plan today! We bring the software, you bring the hardware.

[Create My Free Account](https://gridpane.com/checkout/?plan=core)

