To check quota on WH:

1. SSH into the server.
2. Move to your site directory (replace domain appropriately): `cd /var/www/html/domain/`
3. Run `du -s --block-size=MB --apparent-size`