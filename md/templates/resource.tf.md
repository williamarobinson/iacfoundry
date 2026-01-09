resource "{full_name}" "{resource}" {
  for_each = { for key, value in {variable_name} : key => value if value.enabled }

{required_arguments}

{optional_arguments}

{required_blocks}

{optional_blocks}

  lifecycle {
    prevent_destroy = false
  }
}
